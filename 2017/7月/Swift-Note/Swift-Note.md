# Swift Note


* Objc Swift混编的问题

>属性变量声明

swift 文件中声明的可选值?(基础变量如Bool,Int等)属性，在swift.h 桥接文件中是看不到的，并且通过class_copyPropertyList是获取不到相应的属性值的，针对这种情况需要在swift文件中声明属性的时候不能携带 !和？符号 并且需要在init方法中初始化此变量属性。

```
声明
 var totalDuration:Int
初始化
 override init() {
        self.totalDuration = 0
        super.init()
    }
```

* AnyHashable 类型对应 NSObject类型,Any对应id类型

* Block
>Block 属性声明

```
 var testResponse : (() -> ())?
 var updateBallViewCountdown : ((_ time:Double) -> ())?
```

>Block 设置属性

```
view.blockLogin = {(obj_bolck:String) in
               print(obj_bolck)
            }
```

> Block 防止循环引用

```
通过{[weak self] (value:value) in }  修饰
```
    
    
* 一些常用函数使用

> GCD计时器

```
timer = DispatchSource.makeTimerSource(queue:DispatchQueue.global())
            timer?.scheduleRepeating(deadline: .now(), interval: .seconds(1))
            timer?.setEventHandler(handler: {
                DispatchQueue.main.async {
                    self.timerCallback()
                }
            })
            timer?.resume()
```

          
> 单例

```

    class var sharedInstance: QCBallCountDownTouch {
        struct Static {
            static let instance: QCBallCountDownTouch = QCBallCountDownTouch.init(frame: CGRect.init(x: 0, y: 100, width: 49, height: 49))
        }
        
        return Static.instance
    }
    
``` 

> Guard 保护模式
  
  
* 参考资料

<http://special.csdncms.csdn.net/the-swift-programming-language-in-chinese/Introduction/template/chapter1/02_a_swift_tour.html>

<https://numbbbbb.gitbooks.io/-the-swift-programming-language-/chapter1/01_swift.html>

<http://www.cocoachina.com/special/swift/>

>混编

<https://developer.apple.com/library/content/documentation/Swift/Conceptual/BuildingCocoaApps/MixandMatch.html>
