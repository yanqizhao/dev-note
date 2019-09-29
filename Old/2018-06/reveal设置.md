# reveal设置

打开reveal应用，点击状态栏的Help，选择Integration Guide，获取当前版本的集成指南

![Screen Shot 2018-06-05 at 18.34.56](media/Screen%20Shot%202018-06-05%20at%2018.34.56.png)

以版本4为例，在Xcode中添加`Symbolic Breakpoint`断点，`Symbol`为`UIApplicationMain`，点击`Add Action`，`Action`为`Debugger Command`，内容填入：

> ```
expr (Class)NSClassFromString(@"IBARevealLoader") == nil ? (void *)dlopen("/Applications/Reveal.app/Contents/SharedSupport/iOS-Libraries/RevealServer.framework/RevealServer", 0x2) : ((void*)0)
```

并勾选`Automatically continue after evaluating actions`

![Screen Shot 2018-06-05 at 18.39.08](media/Screen%20Shot%202018-06-05%20at%2018.39.08.png)![Screen Shot 2018-06-05 at 18.39.27](media/Screen%20Shot%202018-06-05%20at%2018.39.27.png)
![Screen Shot 2018-06-05 at 18.40.05](media/Screen%20Shot%202018-06-05%20at%2018.40.05.png)

到此完成了通过断点设置reveal，其他方法包括CocoaPod与链接Framework等可根据指南进行设置。




