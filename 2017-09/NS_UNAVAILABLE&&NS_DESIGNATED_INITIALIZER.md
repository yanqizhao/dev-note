# NS_UNAVAILABLE与NS_DESIGNATED_INITIALIZER的使用

故事是这样发生的。

有一天我写了一个类，这个类中有2个构造方法A和B，在A中调用了B，而使用者在不了解的情况下写了一个子类，在B中调用了A，造成了死循环。

然后我才意识到自己的写法有多么的不规范。

![屏幕快照 2017-09-29 上午11.14.02](media/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202017-09-29%20%E4%B8%8A%E5%8D%8811.14.02.png)


代码如下：

```
// .h
@interface Animal : NSObject

- (instancetype)initWithType:(id)type;

@end

@interface Person : Animal

- (instancetype)initWithName:(NSString *)name;

@end

@interface Student : Person

@end
```


```
// .m
@interface Animal ()

@property (nonatomic, strong) id type;

@end

@implementation Animal

- (instancetype)initWithType:(id)type {
    if (self = [super init]) {
        _type = type;
    }
    return self;
}

@end

@interface Person ()

@property (nonatomic, strong) NSString *name;

@end

@implementation Person

- (instancetype)init {
    if (self = [super initWithType:nil]) {
        
    }
    return self;
}

- (instancetype)initWithName:(NSString *)name {
    if (self = [self init]) {
        _name = name;
    }
    return self;
}

@end

@implementation Student

- (instancetype)init {
    if (self = [self initWithName:@"Peter"]) {
        
    }
    return self;
}

@end
```

动物类与人类是我写的类，而学生类则是别人扩展的。我觉得自己的类写的完全没问题，创建一个动物实例就要知道它的类型type，创建一个人的实例也要知道他的名字name，这不是不言而喻的吗？而学生的实例创建的时候难道不该再声明一个构造方法传入学号或者直接重写人类的构造方法吗？干嘛要重写init方法？

我们就是喜欢想当然，并且超自恋，以为所有人都跟你的想法一样。人家就是要重写init方法你要怎样？两个办法，第一种，告诉他们你的想法有多么的合理多么的明智，写清楚注释，解释明白为什么要这么做，这显然不可能，谁会认真看你的注释！第二种，让你用哪个你就用哪个，不用就报错，自行崩溃，哦也。

修改后的代码如下：

```
// .h
@interface Animal : NSObject

+ (instancetype)new NS_UNAVAILABLE;
- (instancetype)init NS_UNAVAILABLE;
- (instancetype)initWithType:(id)type NS_DESIGNATED_INITIALIZER;

@end

@interface Person : Animal

+ (instancetype)new NS_UNAVAILABLE;
- (instancetype)init NS_UNAVAILABLE;
- (instancetype)initWithName:(NSString *)name NS_DESIGNATED_INITIALIZER;

@end

@interface Student : Person

@end
```


```
// .m
@interface Animal ()

@property (nonatomic, strong) id type;

@end

@implementation Animal

- (instancetype)init {
    if (self = [self initWithType:nil]) {
        
    }
    return self;
}

- (instancetype)initWithType:(id)type {
    if (self = [super init]) {
        _type = type;
    }
    return self;
}

@end

@interface Person ()

@property (nonatomic, strong) NSString *name;

@end

@implementation Person

- (instancetype)initWithType:(id)type {
    if (self = [self initWithName:nil]) {
        
    }
    return self;
}

- (instancetype)initWithName:(NSString *)name {
    if (self = [super initWithType:nil]) {
        _name = name;
    }
    return self;
}

@end

@implementation Student

- (instancetype)initWithName:(NSString *)name {
    if (self = [super initWithName:name]) {
        
    }
    return self;
}

@end
```

![屏幕快照 2017-09-29 上午11.36.05](media/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202017-09-29%20%E4%B8%8A%E5%8D%8811.36.05.png)

这样一来，用两个宏定义就搞定了。几个注意点如下：

1. 当前类需要在禁止子类使用的方法后添加`NS_UNAVAILABLE`，这些方法在代码提示中不会再出现，强行调用则会报错。
2. 当前类需要在预设的构造方法后添加`NS_DESIGNATED_INITIALIZER`。
3. 当前类需要实现父类的预设构造方法，也就是父类中标记了`NS_DESIGNATED_INITIALIZER`的方法，并调用自己的预设构造方法。
4. 当前类的预设构造方法中需要调用父类的预设构造方法。

[代码在这里](https://github.com/yanqizhao/dev-demo/tree/develop/DesignatedInitializer)

参考：

[『Apple API』NS_UNAVAILABLE 与 NS_DESIGNATED_INITIALIZER](http://www.saitjr.com/ios/ios-ns_unavailable-ns_designated_initializer.html)

[Adopting Modern Objective-C](https://developer.apple.com/library/content/releasenotes/ObjectiveC/ModernizationObjC/AdoptingModernObjective-C/AdoptingModernObjective-C.html)

[Xcode 6 Objective-C Modernization](https://useyourloaf.com/blog/xcode-6-objective-c-modernization/)

[正确编写Designated Initializer的几个原则](http://www.starfelix.com/blog/2014/04/13/zheng-que-bian-xie-designated-initializerde-ji-ge-yuan-ze/)

[How To: Objective C Initializer Patterns](https://blog.twitter.com/engineering/en_us/a/2014/how-to-objective-c-initializer-patterns.html)

