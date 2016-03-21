#UIViewController

[TOC]

## UIViewController的初始化

VC的初始化里很重要的一步就是对view属性的初始化，保证到达viewDidLoad的时候view属性非nil。

对于SB创建的VC，VC使用initWithCoder:进行初始化；

其他情况，VC是使用init:方法进行对象初始化，系统提供的UIViewController类init:实现过程中还会调用initWithNibName:bundle:方法完成VC的。



###VC.view的初始化 - loadView

**无特殊情况，视图的初始化工作，可以在viewDidLoad里完成。**



> -(void)loadView; *// This is where subclasses should create their custom view hierarchy if they aren't using a nib. Should never be called directly.*

如果子类VC不是使用nib方式定义其视图层级关系，那么应该在此自定义视图层级关系，不应直接调用。

*说明:* **如果是使用与VC同名的xib初始化VC.view（比如使用SB、VC自动生成的xib），一定不要重写loadView方法。**如果重写了，那么xib里边的视图会失效。

如果真要在此自定义VC.view，一般的做法就是

```objective-c
//NSLog(@"self.view:%@", self.view);//千万不要这么干！！VC.view属性的getter会陷入loadView的死循环里。
CustomView *customView = [[CustomView alloc]initWithFrame:[UIScreen mainScreen].bounds];
//configure the customView ...
self.view =view;
```

```objective-c
@property(null_resettable, nonatomic,strong) UIView *view; // The getter first invokes [self loadView] if the view hasn't been set yet. Subclasses must call super if they override the setter or getter.
//VC中的view属性的getter如果为nil时，那么就会第一时间调loadView去初始化view。
```



### API-loadView的说明

> **You should never call this method directly. The view controller calls this method when its view property is requested but is currently nil. This method loads or creates a view and assigns it to the view property.**

当VC访问view属性并发现其为nil时，就会去调用loadView加载视图，此方法正是为此而创建一个view并赋值给VC.view而生的。




> **If the view controller has an associated nib file, this method loads the view from the nib file. A view controller has an associated nib file if the nibName property returns a non-nil value, which occurs if the view controller was instantiated from a storyboard, if you explicitly assigned it a nib file using the initWithNibName:bundle: method, or if iOS finds a nib file in the app bundle with a name based on the view controller's class name. If the view controller does not have an associated nib file, this method creates a plain UIView object instead.**
> **如果VC已经跟一个nib文件关联，loadView方法会去nib文件里加载视图作为VC的view。一个VC的nibName属性非空就说明已经关联了一个nib文件，**一般出现在使用StoryBoard设计VC、明确使用 initWithNibName:bundle: 去初始化VC、或者iOS在app里发现一个nib文件跟VC类同名。** 最后，如果VC没有关联任何的nib文件，那么loadView方法就会给VC.view创建一个空白的UIView对象。



> **If you use Interface Builder to create your views and initialize the view controller, you must not override this method.**
>
> **You can override this method in order to create your views manually. If you choose to do so, assign the root view of your view hierarchy to the view property. The views you create should be unique instances and should not be shared with any other view controller object. Your custom implementation of this method should not call super.**
>
> **If you want to perform any additional initialization of your views, do so in the viewDidLoad method.**

如果你使用IB来创建你的视图并用来初始化你的VC，切勿重载此方法。

你可以通过重载此方法去手动创建你的视图。如果你这么干了，请把创建的视图的根视图赋值给VC.view。创建出来的视图应该是个独一无二的实例，且请勿与其他VC对象共享之。里边也不应该调用父类的这个方法。

如果你想对视图做一些额外的初始化工作，请在viewDidLoad方法里完成。

总之：**无特殊情况，视图的初始化工作，可以在viewDidLoad里完成。**



## UIViewController的生命周期

vcA 从出现到push到vcB：

```objective-c
 1. A viewDidLoad  
 2. A viewWillAppear  
 3. A viewDidAppear  
 4. B viewDidLoad  
 5. A viewWillDisappear  
 6. B viewWillAppear  
 7. A viewDidDisappear
 8. B viewDidAppear
```

vcB pop回 vcA，则：

```objective-c
1. B viewWillDisappear  
2. A viewWillAppear  
3. B viewDidDisappear  
4. A viewDidAppear  
5. B dealloc//A视图已经出现之后，vcB对象销毁。
```

**值得注意的是，B视图pop回来的时候前一个视图控制器`vcB`在A视图`viewDidAppear`后才被销毁。**




##再见，viewDidUnload方法

*从 iOS 6 开始，viewDidUnload 方法被废弃掉了，应用收到 memory warning 时也不会再调用 viewDidUnload 方法。*

在 iOS6 时，当系统发出 MemoryWarning 时，**系统会自动回收 bitmap 类**。但是不回收 UIView 和 CALayer 类。这样即回收了大部分内



存，又能在需要 bitmap 类时，通过调用 UIView 的 drawRect: 方法重建。如果贸贸然把self.view = nil;那么下次需要用到该视图时就需要重新做loadView的活了，而且还会触发viewDidLoad等等一系列创建视图的方法。

摘自:
 [唐巧的技术博客](http://blog.devtang.com/2013/05/18/goodbye-viewdidunload/)



##关于self.view.frame在viewDidLoad与viewWillApear的差异

基本是因为vc对xib文件的加载是原封不动的尺寸加载这种方式引起的，但是最后都能正确显示是因为self.view的autoresize = W+H，这个自动调整尺寸的属性让frame最后显示时根据屏幕尺寸做了自动调整。
