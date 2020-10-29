---
title: DirectX 中的语音输入
description: 介绍如何在适用于 Windows Mixed Reality 的 DirectX 应用程序中实现语音命令和短语识别。
author: mikeriches
ms.author: mriches
ms.date: 08/04/2020
ms.topic: article
keywords: 演练，语音命令，短语，识别，语音，directx，平台，cortana，windows mixed reality
ms.openlocfilehash: bdd92f79b3dd9677ac5c2c64e532978477ac5bca
ms.sourcegitcommit: 09599b4034be825e4536eeb9566968afd021d5f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/03/2020
ms.locfileid: "91677083"
---
# <a name="voice-input-in-directx"></a>DirectX 中的语音输入

> [!NOTE]
> 本文与旧版 WinRT 本机 Api 相关。  对于新的本机应用项目，建议使用 **[OPENXR API](openxr-getting-started.md)** 。

本文介绍如何在适用于 Windows Mixed Reality 的 DirectX 应用程序中实现 [语音命令](../../design/voice-input.md) 和短语识别。

>[!NOTE]
>本文中的代码片段使用 c + +/CX，而不是 C + + 17 兼容 c + +/WinRT，它用于 [c + + 全息项目模板](creating-a-holographic-directx-project.md)。  概念与 c + +/WinRT 项目等效，但你需要转换代码。

## <a name="use-speechrecognizer-for-continuous-speech-recognition"></a>使用 SpeechRecognizer 进行连续语音识别

本部分介绍如何使用连续语音识别在应用中启用语音命令。 本演练使用 [HolographicVoiceInput](https://go.microsoft.com/fwlink/p/?LinkId=844964) 示例中的代码。 当示例运行时，请用一个已注册颜色命令的名称来更改旋转立方体的颜色。

首先，创建一个新的 *Windows：： Media：： SpeechRecognition：： SpeechRecognizer* 实例。

From *HolographicVoiceInputSampleMain：： CreateSpeechConstraintsForCurrentState* ：

```
m_speechRecognizer = ref new SpeechRecognizer();
```

创建要侦听的识别器的语音命令的列表。 在这里，我们将构造一组命令来更改全息图的颜色。 为方便起见，我们还创建了以后用于命令的数据。

```
m_speechCommandList = ref new Platform::Collections::Vector<String^>();
   m_speechCommandData.clear();
   m_speechCommandList->Append(StringReference(L"white"));
   m_speechCommandData.push_back(float4(1.f, 1.f, 1.f, 1.f));
   m_speechCommandList->Append(StringReference(L"grey"));
   m_speechCommandData.push_back(float4(0.5f, 0.5f, 0.5f, 1.f));
   m_speechCommandList->Append(StringReference(L"green"));
   m_speechCommandData.push_back(float4(0.f, 1.f, 0.f, 1.f));
   m_speechCommandList->Append(StringReference(L"black"));
   m_speechCommandData.push_back(float4(0.1f, 0.1f, 0.1f, 1.f));
   m_speechCommandList->Append(StringReference(L"red"));
   m_speechCommandData.push_back(float4(1.f, 0.f, 0.f, 1.f));
   m_speechCommandList->Append(StringReference(L"yellow"));
   m_speechCommandData.push_back(float4(1.f, 1.f, 0.f, 1.f));
   m_speechCommandList->Append(StringReference(L"aquamarine"));
   m_speechCommandData.push_back(float4(0.f, 1.f, 1.f, 1.f));
   m_speechCommandList->Append(StringReference(L"blue"));
   m_speechCommandData.push_back(float4(0.f, 0.f, 1.f, 1.f));
   m_speechCommandList->Append(StringReference(L"purple"));
   m_speechCommandData.push_back(float4(1.f, 0.f, 1.f, 1.f));
```

你可以使用不在字典中的拼音词来指定命令。

```
m_speechCommandList->Append(StringReference(L"SpeechRecognizer"));
   m_speechCommandData.push_back(float4(0.5f, 0.1f, 1.f, 1.f));
```

若要将命令列表加载到语音识别器的约束列表中，请使用 [SpeechRecognitionListConstraint](https://msdn.microsoft.com/library/windows/apps/windows.media.speechrecognition.speechrecognitionlistconstraint.aspx) 对象。

```
SpeechRecognitionListConstraint^ spConstraint = ref new SpeechRecognitionListConstraint(m_speechCommandList);
   m_speechRecognizer->Constraints->Clear();
   m_speechRecognizer->Constraints->Append(spConstraint);
   create_task(m_speechRecognizer->CompileConstraintsAsync()).then([this](SpeechRecognitionCompilationResult^ compilationResult)
   {
       if (compilationResult->Status == SpeechRecognitionResultStatus::Success)
       {
           m_speechRecognizer->ContinuousRecognitionSession->StartAsync();
       }
       else
       {
           // Handle errors here.
       }
   });
```

订阅语音识别器的[SpeechContinuousRecognitionSession](https://msdn.microsoft.com/library/windows/apps/windows.media.speechrecognition.speechcontinuousrecognitionsession.aspx)上的[ResultGenerated](https://msdn.microsoft.com/library/windows/apps/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated.aspx)事件。 此事件将在你已识别到你的某个命令时通知你的应用程序。

```
m_speechRecognizer->ContinuousRecognitionSession->ResultGenerated +=
       ref new TypedEventHandler<SpeechContinuousRecognitionSession^, SpeechContinuousRecognitionResultGeneratedEventArgs^>(
           std::bind(&HolographicVoiceInputSampleMain::OnResultGenerated, this, _1, _2)
           );
```

*OnResultGenerated* 事件处理程序接收 [SpeechContinuousRecognitionResultGeneratedEventArgs](https://msdn.microsoft.com/library/windows/apps/windows.media.speechrecognition.speechcontinuousrecognitionresultgeneratedeventargs.aspx)实例中的事件数据。 如果置信度大于你定义的阈值，应用应注意到事件发生。 保存事件数据，以便可以在后续的更新循环中使用它。

从 *HolographicVoiceInputSampleMain* ：

```
// Change the cube color, if we get a valid result.
   void HolographicVoiceInputSampleMain::OnResultGenerated(SpeechContinuousRecognitionSession ^sender, SpeechContinuousRecognitionResultGeneratedEventArgs ^args)
   {
       if (args->Result->RawConfidence > 0.5f)
       {
           m_lastCommand = args->Result->Text;
       }
   }
```

在我们的示例代码中，我们将根据用户的命令更改旋转全息图多维数据集的颜色。

From *HolographicVoiceInputSampleMain：： Update* ：

```
// Check for new speech input since the last frame.
   if (m_lastCommand != nullptr)
   {
       auto command = m_lastCommand;
       m_lastCommand = nullptr;

       int i = 0;
       for each (auto& iter in m_speechCommandList)
       {
           if (iter == command)
           {
               m_spinningCubeRenderer->SetColor(m_speechCommandData[i]);
               break;
           }

           ++i;
       }
   }
```

## <a name="use-one-shot-recognition"></a>使用 "一次拍摄" 识别

你可以配置语音识别器来侦听用户讲述的短语或句子。 在这种情况下，我们将应用 *SpeechRecognitionTopicConstraint* ，告知语音识别器所需的输入类型。 下面是此方案的应用工作流：
1. 你的应用程序将创建 SpeechRecognizer，提供 UI 提示，并开始侦听讲述命令。
2. 用户讲述一个短语或句子。
3. 用户的语音识别发生，并将结果返回到应用。 此时，你的应用程序应提供 UI 提示以指示已发生识别。
4. 根据你想要响应的置信度和语音识别结果的置信度，你的应用程序可以处理结果并相应地做出响应。

本部分介绍如何创建 SpeechRecognizer、编译约束和侦听语音输入。

下面的代码编译主题约束，这种情况下，它针对 web 搜索进行了优化。

```
auto constraint = ref new SpeechRecognitionTopicConstraint(SpeechRecognitionScenario::WebSearch, L"webSearch");
   m_speechRecognizer->Constraints->Clear();
   m_speechRecognizer->Constraints->Append(constraint);
   return create_task(m_speechRecognizer->CompileConstraintsAsync())
       .then([this](task<SpeechRecognitionCompilationResult^> previousTask)
   {
```

如果编译成功，则可以继续语音识别。

```
try
       {
           SpeechRecognitionCompilationResult^ compilationResult = previousTask.get();

           // Check to make sure that the constraints were in a proper format and the recognizer was able to compile it.
           if (compilationResult->Status == SpeechRecognitionResultStatus::Success)
           {
               // If the compilation succeeded, we can start listening for the user's spoken phrase or sentence.
               create_task(m_speechRecognizer->RecognizeAsync()).then([this](task<SpeechRecognitionResult^>& previousTask)
               {
```

然后，将结果返回到应用程序。 如果我们完全相信，我们可以处理该命令。 此代码示例处理至少具有中等置信度的结果。

```
try
                   {
                       auto result = previousTask.get();

                       if (result->Status != SpeechRecognitionResultStatus::Success)
                       {
                           PrintWstringToDebugConsole(
                               std::wstring(L"Speech recognition was not successful: ") +
                               result->Status.ToString()->Data() +
                               L"\n"
                               );
                       }

                       // In this example, we look for at least medium confidence in the speech result.
                       if ((result->Confidence == SpeechRecognitionConfidence::High) ||
                           (result->Confidence == SpeechRecognitionConfidence::Medium))
                       {
                           // If the user said a color name anywhere in their phrase, it will be recognized in the
                           // Update loop; then, the cube will change color.
                           m_lastCommand = result->Text;

                           PrintWstringToDebugConsole(
                               std::wstring(L"Speech phrase was: ") +
                               m_lastCommand->Data() +
                               L"\n"
                               );
                       }
                       else
                       {
                           PrintWstringToDebugConsole(
                               std::wstring(L"Recognition confidence not high enough: ") +
                               result->Confidence.ToString()->Data() +
                               L"\n"
                               );
                       }
                   }
```

使用语音识别时，请注意可能表明用户已在系统隐私设置中关闭麦克风的例外情况。 这可能发生在初始化或识别期间。

```
catch (Exception^ exception)
                   {
                       // Note that if you get an "Access is denied" exception, you might need to enable the microphone
                       // privacy setting on the device and/or add the microphone capability to your app manifest.

                       PrintWstringToDebugConsole(
                           std::wstring(L"Speech recognizer error: ") +
                           exception->ToString()->Data() +
                           L"\n"
                           );
                   }
               });

               return true;
           }
           else
           {
               OutputDebugStringW(L"Could not initialize predefined grammar speech engine!\n");

               // Handle errors here.
               return false;
           }
       }
       catch (Exception^ exception)
       {
           // Note that if you get an "Access is denied" exception, you might need to enable the microphone
           // privacy setting on the device and/or add the microphone capability to your app manifest.

           PrintWstringToDebugConsole(
               std::wstring(L"Exception while trying to initialize predefined grammar speech engine:") +
               exception->Message->Data() +
               L"\n"
               );

           // Handle exceptions here.
           return false;
       }
   });
```

> [!NOTE]
> 可使用多个预定义的 [SpeechRecognitionScenarios](https://msdn.microsoft.com/library/windows/apps/windows.media.speechrecognition.speechrecognitionscenario.aspx) 来优化语音识别。

* 若要优化听写，请使用听写方案。<br/>
   ```
   // Compile the dictation topic constraint, which optimizes for speech dictation.
   auto dictationConstraint = ref new SpeechRecognitionTopicConstraint(SpeechRecognitionScenario::Dictation, "dictation");
   m_speechRecognizer->Constraints->Append(dictationConstraint);
   ```

* 对于语音 web 搜索，请使用以下特定于 web 的方案约束。

   ```
   // Add a web search topic constraint to the recognizer.
   auto webSearchConstraint = ref new SpeechRecognitionTopicConstraint(SpeechRecognitionScenario::WebSearch, "webSearch");
   speechRecognizer->Constraints->Append(webSearchConstraint);
   ```

* 使用窗体约束填写表单。 在这种情况下，最好应用自己的语法，用于填写表单。

   ```
   // Add a form constraint to the recognizer.
   auto formConstraint = ref new SpeechRecognitionTopicConstraint(SpeechRecognitionScenario::FormFilling, "formFilling");
   speechRecognizer->Constraints->Append(formConstraint );
   ```
* 您可以以 SRGS 格式提供自己的语法。

## <a name="use-continuous-recognition"></a>使用连续识别

有关连续听写方案，请参阅 [Windows 10 UWP 语音代码示例](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/SpeechRecognitionAndSynthesis/cpp/Scenario_ContinuousDictation.xaml.cpp)。

## <a name="handle-quality-degradation"></a>处理质量降级

环境条件有时会干扰语音识别。 例如，房间可能太干扰，或者用户可能会说声音太大。 只要有可能，语音识别 API 就会提供导致质量降低的条件的相关信息。 此信息通过 WinRT 事件推送到应用。 下面的示例演示如何订阅此事件。

```
m_speechRecognizer->RecognitionQualityDegrading +=
       ref new TypedEventHandler<SpeechRecognizer^, SpeechRecognitionQualityDegradingEventArgs^>(
           std::bind(&HolographicVoiceInputSampleMain::OnSpeechQualityDegraded, this, _1, _2)
           );
```

在我们的代码示例中，我们将条件信息写入调试控制台。 应用可能需要通过 UI、语音合成和另一种方法向用户提供反馈。 或者，当语音被暂时降低质量的中断时，可能需要以不同的方式运行。

```
void HolographicSpeechPromptSampleMain::OnSpeechQualityDegraded(SpeechRecognizer^ recognizer, SpeechRecognitionQualityDegradingEventArgs^ args)
   {
       switch (args->Problem)
       {
       case SpeechRecognitionAudioProblem::TooFast:
           OutputDebugStringW(L"The user spoke too quickly.\n");
           break;

       case SpeechRecognitionAudioProblem::TooSlow:
           OutputDebugStringW(L"The user spoke too slowly.\n");
           break;

       case SpeechRecognitionAudioProblem::TooQuiet:
           OutputDebugStringW(L"The user spoke too softly.\n");
           break;

       case SpeechRecognitionAudioProblem::TooLoud:
           OutputDebugStringW(L"The user spoke too loudly.\n");
           break;

       case SpeechRecognitionAudioProblem::TooNoisy:
           OutputDebugStringW(L"There is too much noise in the signal.\n");
           break;

       case SpeechRecognitionAudioProblem::NoSignal:
           OutputDebugStringW(L"There is no signal.\n");
           break;

       case SpeechRecognitionAudioProblem::None:
       default:
           OutputDebugStringW(L"An error was reported with no information.\n");
           break;
       }
   }
```

如果未使用 ref 类创建 DirectX 应用，则必须先取消订阅该事件，然后才能释放或重新创建语音识别器。 HolographicSpeechPromptSample 有一个例程，用于停止识别和取消订阅事件。

```
Concurrency::task<void> HolographicSpeechPromptSampleMain::StopCurrentRecognizerIfExists()
   {
       return create_task([this]()
       {
           if (m_speechRecognizer != nullptr)
           {
               return create_task(m_speechRecognizer->StopRecognitionAsync()).then([this]()
               {
                   m_speechRecognizer->RecognitionQualityDegrading -= m_speechRecognitionQualityDegradedToken;

                   if (m_speechRecognizer->ContinuousRecognitionSession != nullptr)
                   {
                       m_speechRecognizer->ContinuousRecognitionSession->ResultGenerated -= m_speechRecognizerResultEventToken;
                   }
               });
           }
           else
           {
               return create_task([this]() { m_speechRecognizer = nullptr; });
           }
       });
   }
```

## <a name="use-speech-synthesis-to-provide-audible-prompts"></a>使用语音合成提供可听见的提示

全息语音示例使用语音合成向用户提供可听见的指令。 本部分介绍如何创建合成语音样本，并通过 HRTF 音频 Api 将其播放回来。

请求短语输入时应提供自己的语音提示。 提示还可以帮助指示何时可以为连续识别方案口述语音命令。 下面的示例演示如何使用语音合成器执行此操作。 你还可以使用预先录制的语音剪辑、视觉对象 UI 或另一个指示符，例如在提示不是动态的情况下。

首先，创建 SpeechSynthesizer 对象。

```
auto speechSynthesizer = ref new Windows::Media::SpeechSynthesis::SpeechSynthesizer();
```

还需要包含要合成的文本的字符串。

```
// Phrase recognition works best when requesting a phrase or sentence.
   StringReference voicePrompt = L"At the prompt: Say a phrase, asking me to change the cube to a specific color.";
```

通过 SynthesizeTextToStreamAsync 以异步方式合成语音。 在这里，我们启动了一个异步任务来合成语音。

```
create_task(speechSynthesizer->SynthesizeTextToStreamAsync(voicePrompt), task_continuation_context::use_current())
       .then([this, speechSynthesizer](task<Windows::Media::SpeechSynthesis::SpeechSynthesisStream^> synthesisStreamTask)
   {
       try
       {
```

语音合成作为字节流发送。 我们可以使用该字节流来初始化 XAudio2 的声音。 对于我们的全息代码示例，我们将它作为 HRTF 音频效果播放。

```
Windows::Media::SpeechSynthesis::SpeechSynthesisStream^ stream = synthesisStreamTask.get();

           auto hr = m_speechSynthesisSound.Initialize(stream, 0);
           if (SUCCEEDED(hr))
           {
               m_speechSynthesisSound.SetEnvironment(HrtfEnvironment::Small);
               m_speechSynthesisSound.Start();

               // Amount of time to pause after the audio prompt is complete, before listening
               // for speech input.
               static const float bufferTime = 0.15f;

               // Wait until the prompt is done before listening.
               m_secondsUntilSoundIsComplete = m_speechSynthesisSound.GetDuration() + bufferTime;
               m_waitingForSpeechPrompt = true;
           }
       }
```

与语音识别一样，如果出现问题，语音合成就会引发异常。

```
catch (Exception^ exception)
       {
           PrintWstringToDebugConsole(
               std::wstring(L"Exception while trying to synthesize speech: ") +
               exception->Message->Data() +
               L"\n"
               );

           // Handle exceptions here.
       }
   });
```

## <a name="see-also"></a>请参阅
* [语音应用设计](https://msdn.microsoft.com/library/dn596121.aspx)
* [SpeechRecognitionAndSynthesis 示例](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/SpeechRecognitionAndSynthesis)
