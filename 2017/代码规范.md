# 代码规范

##一：基本代码命名

###1.通用原则

尽量清晰又简洁，无法两全时清晰更重要，可读性优先级更高。

insertObject:atIndex:   好的

insert:at               坏的

removeObject:          	 好的

remove:				    坏的


通常不应缩写名称，即使方法名很长也应完整拼写

```
destinationSelection   好
destSel					坏
```

避免一些歧义

displayName 显示一个名字还是展示一个标题

####1.2 一致性

尽量和Cocoa编程接口命名一致

当某个类使用了多态的时候，一致性很重要，不同类里，功能相同的方法命名也应相同

-(NSInteger)tag

####1.3 避免一些自引用

譬如本身就是某一个类的对象，但是在命名的时候又额外的扩展了

NSStringObject  错误 

NSString   正确

但是有些是应该忽略此规则的如Notifaction和Mask

NSUnderlineByWordMask 

NSTableViewColumnDidMoveNotifaction

###2.前缀

前缀可以防止使用一些第三方库之类的文件发生冲突，一般来说前缀使用大写字母2个到3个不要使用下划线等

命名类、协议、函数、常量和typedef结构体时使用前缀，方法名和结构体不要使用前缀
	
###3.书写规则

在命名API元素时， 使用驼峰命名法（如runTheWordsTogether），并注意以下书写约定：
方法名
小写第一个字母，大写之后所有单词的首字母，不使用前缀
如果方法名以一个众所周知的大写缩略词开始，该规则不适用

fileExistsAtPath:isDirectory:

函数及常量名

使用与其关联类相同的前缀，并大写首字母
NSRunAlertPanel
NSCellDisabled

标点符号

由多个单词组成的名称，别使用标点符号作为名称的一部分
分隔符（下划线、破折号等）也不能使用
避免使用下划线作为私有方法的前缀，Apple保留这一方式的使用
强行使用可能会导致命名冲突，即Apple已有的方法被覆盖，这会导致灾难性后果
实例变量使用下划线作为前缀还是允许的

###4.class与protocol命名

类名命名的时候最好包含一个名词，这样可以表明此类是什么，有什么意思
如NSString、NSDate、NSScanner、UIApplication、UIButton

对与protocol类的命名可以加上ing的形式或者以protocol后缀区分

关联class的protocol

一些protoco聚集了一堆无关方法，并试图与某个class关联在一起，由这个class来主导
这种protocol与class同名
如NSObject protocol


###5.头文件

可以声明一些宏定义或者常亮或者某一模块的枚举之类的在一个头文件中

##二：方法命名

方法要用小写字母开头之后单词大写，如果方法代表接收的动作，以动词开头，不要使用do或者does作为名字一部分，助动词没有实际意义

-(void)invokeWithTarget:(id)target;
-(void)selectTabViewItem:(NSTabViewItem *)tabViewItem

方法返回接收者的属性的时候，要以接收者+接收者属性返回，如果没有返回多个值的话尽量不要加get

-(CGFloat)cellHeight;


确保参数之前的关键字充分描述了参数的意义

-(id)viewWithTag:(NSInteger)tag;

不要使用and链接参数名

如果property表示为名词，格式如下

-(type)noun;

-(void)setNoun:(type)aNoun; 
 
-(BOOL)isAdjective;


###delegate 方法

如果有多个参数回调的时候可以在首个参数后面加上对象名字

-(BOOL)tableView:(NSTableView *)tableView shouldSelectRow:(int)row; 

使用did或者will通知delegate

-(void)browserDidScroll:(NSBrowser *)sender;

-(NSUndoManager *)windowWillReturnUndoManager:(NSWindow *)window;


询问delegate是否可以执行某个行为时可以使用 did 或 will，不过 should 更完美  

-(BOOL)windowShouldClose:(id)sender;


##三：属性以及其他命名
###1.属性命名
属性命名尽可能的指定是否可读

@property (nonatomic, assign, readonly) BOOL isLogined;

如果属性表示一个名词或者动词的时候

@property (strong) NSString *title;
@property (assign) BOOL showsAlpha;

如果是一个形容词

@property (assign, getter=isEditable) BOOL editable;


枚举常量可以使用苹果 官方风格

```
typedef enum _NSMatrixMode {
    NSRadioModeMatrix            = 0,
    NSHighlightModeMatrix       = 1,           
    NSListModeMatrix            = 2, 
    NSTrackModeMatrix           = 3
} NSMatrixMode;
```

###通知常量命名
通知可以用extern在某个类里边声明，之后再实现的类里边如下引用就行

extern NSString *QCUserDidLogoutNotification;


###不可变的常量命名

可以在前边加上static const修饰

static const NSTimeInterval kAnimationDuration = 0.3;

##四：缩写
设计编程接口时通常不应使用缩写，被广泛使用的缩写名称除外

##五：条件判断

普通if else 判断可以省略 ==YES之类的

```
if (someObject) { ... } 
if (!someObject) { ... }

if (someObject == YES) { ...} 
if (someObject != nil) { ...}
```

复杂的逻辑判断可以腾出一个方法专门处理

嵌套判断可以使用如下

```
if (!user.UserName) return NO;
if (!user.Password) return NO;
if (!user.Email) return NO;
 
return YES;
```


