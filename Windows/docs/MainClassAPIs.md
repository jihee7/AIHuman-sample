# Main Class APIs

The APIs of the main classes of AI Human SDK are briefly described.

<br/>

## AIHuman.Media.AIPlayer

| Modifier and Type                    | Method / Property Description                                |
| :----------------------------------- | ------------------------------------------------------------ |
| `ctor`                               | `AIPlayer(IAIPlayerCallback callback)` Create AIPlayer with Default AI and register callback for state monitoring. (valid only when authentication is complete) |
| `ctor`                               | `AIPlayer(string aiName, IAIPlayerCallback callback)` Creates AIPlayer with an AI model defined in aiName and registers callback for state monitoring. (valid only when authentication is complete) |
| `AIHuman.Media.AIPlayerView`         | `GetObject()` It is the actual Control object to be linked(binding) with the View (Xaml) of the Cutom App. |
| `void`                               | `Pause()` Pauses speaking.                                    |
| `void`                               | `Preload(string[] sentences)` Prepare the sentences to be spoken in advance. |
| `void`                               | `Preload(AIClipSet[] clips)` Prepare the clips to be play in advance. |
| `void`                               | `Dispose()` Called when destroying AIPlayer.                 |
| `void`                               | `Resume()` Continue speaking again from when it was paused.   |
| `void`                               | `Send(string[] sentences)` Let the AI speak. (using pure-text string) |
| `void`                               | `Send(AIClipSet[] clips)` Let the AI play. (using AIHuman.Common.Model.AIClipSet) |
| `void`                               | `StopSpeaking()` Stop the current conversation. It also deletes the content in the speaking queue. |
| `float`                              | `Speed { get; set; }` Get or Set the AI's speech rate.       |
| `float`                              | `Scale { get; set; }` Get or Set the AI's scale.             |
| `AIHuman.Common.Margin`              | `Margin { get; set; }` Get or Set the AI's margin.           |
| `System.Windows.Controls.MediaState` | `PlayerState { get; }` Get the state of AIPlayer             |
| `string`                             | `AIName { get; }` Get the AI name.                           |
| `Collection<AIGesture>`              | `GetGestures()` Get a collection of gesture. (available gestures) |
| `Collection<CustomVoice>`            | `GetCustomVoices()` Get a collection of custom voice. (available custom voices) |
| `bool`                               | `SetCustomVoice(CustomVoice cv)` Set AI's voice to cv. return true if success.|
| `CustomVoice`                        | `FindCustomVoice(string id)` Find CustomVoice by id. return null if there is none. |

<br/>

## AIHuman.Interface.IAIPlayerCallback

| Modifier and Type | Method and Description                                       |
| ----------------- | ------------------------------------------------------------ |
| `void`            | `OnAIPlayerError(AIError error)` Reporting an error occurred in AIPlayer |
| `void`            | `OnAIPlayerResLoadingProgressed(int current, int total)` Reporting the resource loading progress of AIPlayer |
| `void`            | `OnAIStateChanged(AIState state)` Reporting the changed state of AI |

<br/>

## AIHuman.Core.AIAPI

| Modifier and Type                | Method and Description                                       |
| -------------------------------- | ------------------------------------------------------------ |
| ` void`                          | `AuthStart(string appId, string userKey, string uuid, string platform, Action<JToken, string> onComplete)` Attempts to authenticate with the issued userKey. It passes the response to CallBack(onComplete) and if successful, you can get a usable AI model. |
| `bool`                           | `GenerateToken(string appId, string userKey, string uuid, string platform)` Attempts to authenticate to the server with this information and returns true if successful. |
| `Newtonsoft.Json.Linq.JObject`   | `GetAIList()` Get a list of available AI models.             |
| `AIHuman.Common.AIModelData`     | `GetDefaultAIData()` Get the default AI information.         |
| `string[]`                       | `GetSampleTexts(string aiName)` Get AI sample sentences using aiName. |
| `string[]`                       | `GetSampleTextList(string languageCode)` Get the list of sample texts for the language from server. |
| `AIHuman.Common.Model.AIClipSet` | `CreateClipSet(string speechText, string gestureName = "", CustomVoice customVoice = null)` Create AIClipSet Object. |

<br/>

## AIHuman.Common.Model.AIClipSet

| Modifier and Type | Method and Description                                       |
| ----------------- | ------------------------------------------------------------ |
| `enum`            | `ClipType` Clipset types are as follows.<br />- CLIP_SPEECH: Clip only for speech without gestures <br />- CLIP_GESTURE: Gesture only Clip<br />- CLIP_SPEECH_GESTURE: Clip for speech with gestures |
| `ClipType`           | `Type { get; }` Get the clip type set in the AIClipSet.               |
| `string`             | `SpeechText { get; }` Get the sentence set in the AIClipSet.               |
| `string`             | `GestureName { get; }` Get the gesture name set in the AIClipSet.               |
| `string`             | `ClipId { get; }` Get the ID set in the AIClipSet.               |

<br/>

## AIHuman.Common.Model.AIGesture

| Modifier and Type    | Method and Description                                       |
| -------------------- | ------------------------------------------------------------ |
| `string`             | `Name { get; }` Get the name of the gesture.               |
| `bool`               | `EnableSpeech { get; }` Get whether the gesture is speech-enabled. Returns true if gesture with speech is possible. |
| `AIClipSet.ClipType` | `GetClipType()` Get the recommended clip type when using the gesture.               |
