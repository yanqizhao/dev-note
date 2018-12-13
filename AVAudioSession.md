# AVAudioSession

https://developer.apple.com/library/archive/qa/qa1882/_index.html

该类是系统提供的一个单例类，供开发者用来与其他应用以及系统共同管理设备音频。

系统默认的音频设置如下：

* 支持播放音频，但不支持录音(tvOS本就不支持录音)
* 在iOS系统下，设备置为静音状态时在播放的音频会被暂停
* 在iOS系统下，锁定设备时在播放的音频会被暂停
* 当前app在播放音频时，任何后台的音频都会被暂停

游戏类app音频建议：

* 建议使用以下category：AVAudioSessionCategoryAmbient、AVAudioSessionCategorySoloAmbient，当用户打开其他app或锁屏，游戏app应该停止播放声音，并且用户需要在玩游戏的同时可以听后台音乐。
* 当应用进入前台时，激活`audio session`
* 可以与其他app混响
* 若没有其他app播放后台声音时，游戏应用可以播放背景音乐
* 当焦点被归还时尝试重新激活声音
* 使用`secondaryAudioShouldBeSilencedHint`属性判断是否重新播放后台音乐
* 忽略音频输出途径的更改
* 在应用启动播放视频前，设置`category`

音视频app建议：

* 在前台时，当用户触发音视频播放时，激活`audio session`
* 在前台时，保持激活状态
* 若没有播放音视频并退到后台，就释放掉焦点
* 当被打断时，更新ui来表示音视频被暂停了，不要释放焦点
* 监听`AVAudioSessionInterruptionNotification`通知以便收到中断提醒，当中断结束，不要重新播放音视频，除非你的app优先于其他app
* 当被没有plug的设备切换音频输出路径，暂停播放，但不要释放焦点
* 若从挂起到前台时，处于未激活状态，当用户重新播放时，激活`audio session`
* 打开后台flag `UIBackgroundModes`
* 注册远程控制并且提供合适的媒体播放信息
* 使用`MPVolumeView`对象展示系统音量条
* 使用后台任务而不是静音流来保证应用被挂起
* 向用户请求录音权限`requestRecordPermission:`，不要依赖系统
* 需要录音时使用`AVAudioSessionCategoryPlayAndRecord`而不是`AVAudioSessionCategoryRecord`

AVAudioSessionSilenceSecondaryAudioHintNotification

AVAudioSessionInterruptionWasSuspendedKey

