# iOS-开发问题集锦
1.Operation not permitted
解决方案：在项目Build Settings中搜索"user script sandboxing"选项，将其值改为"No"可解决相关权限问题

2.UIApplicationInvalidInterfaceOrientation崩溃
崩溃描述： Supported orientations has no common orientation with the application, and [UdeskBaseNavigationViewController shouldAutorotate] is returning YES
解决方案：屏幕旋转问题 在目标Controller增加 shouldAutorotate { return no }

3.dyld: Library not loaded崩溃，现象描述打开app直接崩溃

<img width="433" height="235" alt="截屏2025-11-03 18 23 52" src="https://github.com/user-attachments/assets/79da14c3-6528-4370-9e8b-a1bf3fe80cc8" />

解决步骤：打开app崩溃几次——去手机的隐私分析中查看崩溃记录可查看有问题的动态库

![IMG_0003](https://github.com/user-attachments/assets/3e0dbba8-db35-447e-ad47-5a9f6fd9ac8c)

结果：第三方库系统版本不兼容（升级或者降级版本）

4.如何给低版本第三方库增加privacyInfo(解决ITMS-91061: Missing privacy manifest)

  (1)选中pods工程下SDWebImage文件夹
  
  <img width="213" height="73" alt="image" src="https://github.com/user-attachments/assets/2b5c42ec-f6a5-43c4-a0ed-26fc0082e608" />
  
  (2)Command+N创建如下文件：
  
  <img width="543" height="334" alt="image" src="https://github.com/user-attachments/assets/384aba05-7b09-452f-b8f4-f69060f71b40" />
  
  (3)下一步后，文件名不用更改，也不能更改，SDWebImage进行勾选，如下图
  
  <img width="389" height="349" alt="image" src="https://github.com/user-attachments/assets/11fd307c-6442-489b-832e-300a590012ba" />
  
  (4)确认后，SDWebImage文件夹下会多出PrivacyInfo文件，如下图：
  
  <img width="276" height="140" alt="image" src="https://github.com/user-attachments/assets/8a0adc32-09b8-4747-a81d-b2531f007c33" />
  
  (5)去高版本的三方库下载privacyInfo，复制文件内容。加入低版本文件中。
  (6) ios 尽量避免gif动图，可以使用json动画代替，会造成cpu大量消耗。

5.iOS循环引用问题：Timer的使用必须遵循初始化一次，就要释放一次。例子：
override func viewWillAppear(_ animated: Bool) {
        super.viewWillAppear(animated)
        if isPlaying {
            //endPlayVideoTimer()
            timer = Timer.scheduledTimer(timeInterval: 3.0, target: self, selector: #selector(threeSecondTimeAction), userInfo: nil, repeats: true)
            RunLoop.current.add(timer!, forMode: .common)
            timer?.fire()
        }
    }
    会早造成控制器无法释放，猜测原因timer被加入了Runlop,如果多次调用viewWillAppear，每次创建新对象时，旧timer没有释放，引用计数不为0，对self依然有有引用，导致控制器不能释放。

6.WKWebView push 完成之后底部有96pt的空白高度（tabbar高度）原因safeArea问题，解决webView?.scrollView.contentInsetAdjustmentBehavior = .never

7.如何禁用深色模式：info.plist中增加Key-UIUserInterfaceStyle（Appearance） = Light
  
# ios开发工具
1.png转webp：https://anywebp.com/png-to-webp

# iosUI
旋转适配

一、系统提供的旋转适配方法：

（1）AppDelegate中提供的supportedInterfaceOrientationsFor方法

（2）info.plist中提供的Supported interface orientations（iOS手机）（Supported interface orientations (iPad)）（ipad相关）注意Info.plist中的设置是与工程中General下deployment Info保持一致的

（3）UIViewController中的supportedInterfaceOrientations

（4）iOS13以上提供的UIWindowScene中的windowScene.requestGeometryUpdate（iOS16.0以上设置横竖屏）

二、旋转方法的优先级

 （1）AppDelegate中提供的supportedInterfaceOrientationsFor的优先级最高，即使在info或者deploymentInfo中设置竖屏（Portrait (bottom home button)），但在AppDelegate中设置all，设备依然可以旋转。
 
 （2）如果AppDelegate中不重写supportedInterfaceOrientationsFor，优先级为info(deploymentInfo)>UIViewController(公共的TabbarCotroller>公共NavigationBarController>公共UIViewController>具体UIViewController)重写supportedInterfaceOrientations,可以理解为取supportedInterfaceOrientations的交集。
 
 （3）iOS13.0以后由于引入多任务模式导致整体窗口布局改变：
 
    iOS13前后的UI框架变化：
<img width="1280" height="402" alt="13以前的窗口框架" src="https://github.com/user-attachments/assets/9d3412e1-75e7-417a-a991-a39514a57453" />
<img width="1280" height="551" alt="iOS13 0以后的窗口框架" src="https://github.com/user-attachments/assets/8c1f475d-f1cc-461e-9e53-039bdc231224" />

如果ipad处于多任务模式下，强制竖屏将只能控制UIWindowScene下的竖屏。无法控制设备整体的强制竖屏，只能适配横屏。iOS16.0 以上强制竖屏设置windowScene.requestGeometryUpdate()方法。

let prefs = UIWindowScene.GeometryPreferences.iOS(interfaceOrientations: [.portrait])

windowScene.requestGeometryUpdate(prefs) { error in
}








 
