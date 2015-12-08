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

动态创建一个label
```

30
down vote
accepted
Does the following work ?

UIFont * customFont = [UIFont fontWithName:ProximaNovaSemibold size:12]; //custom font
NSString * text = [self fromSender];

CGSize labelSize = [text sizeWithFont:customFont constrainedToSize:CGSizeMake(380, 20) lineBreakMode:NSLineBreakByTruncatingTail];

UILabel *fromLabel = [[UILabel alloc]initWithFrame:CGRectMake(91, 15, labelSize.width, labelSize.height)];
fromLabel.text = text;
fromLabel.font = customFont;
fromLabel.numberOfLines = 1;
fromLabel.baselineAdjustment = UIBaselineAdjustmentAlignBaselines; // or UIBaselineAdjustmentAlignCenters, or UIBaselineAdjustmentNone
fromLabel.adjustsFontSizeToFitWidth = YES;
fromLabel.adjustsLetterSpacingToFitWidth = YES;
fromLabel.minimumScaleFactor = 10.0f/12.0f;
fromLabel.clipsToBounds = YES;
fromLabel.backgroundColor = [UIColor clearColor];
fromLabel.textColor = [UIColor blackColor];
fromLabel.textAlignment = NSTextAlignmentLeft;
[collapsedViewContainer addSubview:fromLabel];
edit : I believe you may encounter a problem using both adjustsFontSizeToFitWidth and minimumScaleFactor. The former states that you also needs to set a minimumFontWidth (otherwhise it may shrink to something quite unreadable according to my test), but this is deprecated and replaced by the later.

edit 2 : Nevermind, outdated documentation. adjustsFontSizeToFitWidth needs minimumScaleFactor, just be sure no to pass it 0 as a minimumScaleFactor (integer division, 10/12 return 0). Small change on the baselineAdjustment value too.

shareimprove this answer
edited Jul 23 '13 at 15:04
answered Jul 23 '13 at 14:49

Nerkatel
1,083720
  	 	
I would think it would, but using the above, the label doesn't even appear. – user1697845 Jul 23 '13 at 14:53
  	 	
Try commenting out adjutsFontSizeToFitWidth – Nerkatel Jul 23 '13 at 14:55
  	 	
Got it. Change MIN_SCALE_FACTOR to 10.0f/12.0f – Nerkatel Jul 23 '13 at 15:02
  	 	
still doesn't appear in the view. I tried commenting out all the "adjustsTo..." in my previous code, and I still have the same original issue. – user1697845 Jul 23 '13 at 15:03
  	 	
could you break after the addSubview and check that both objects exist and log their frame ? – Nerkatel Jul 23 '13 at 15:08 
```
