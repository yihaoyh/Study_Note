# iOS开发学习
- 对象属性(@property)
@synthesize 定义属性的Getter和Setter
例如
```
//AppDelegate.h
@interface AppDelegate : NSObject <UIApplicationDelegate>{
}
@property (nonatomic, retain) IBOutlet UIWindow * window
@end
```
在类实现代码中通过关键字@synthesize定义属性的Getter和Setter。
```
// AppDelegate.m
@implementaion AppDelegate
@synthesize window;
...
@end
```
属性还可以设置访问权限(readonly)，内存管理(retain),线程管理(nonatomic)


- category
通过不增加子类的方法给原来的类增加接口。
例如
```
SomeClass.h
@interface SomeClass : NSObject{
}
-(void) print;
@end 
```
如果想在不修改该类，不新增子类的情况下，给该类增加一个hello方法，则可以
```
＃import "SomeClass.h"
@interface SomeClass (Hello)
-(void)hello;
@end
```
实现代码如下
```
#import "SomeClass+Hello.h"
@implementationSomeClass (Hello)
-(void)hello{
    NSLog (@"name：%@ ", @"Jacky");
}
@end 
```