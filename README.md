# iOS-开发问题集锦
1.Operation not permitted
解决方案：在项目Build Settings中搜索"user script sandboxing"选项，将其值改为"No"可解决相关权限问题

2.UIApplicationInvalidInterfaceOrientation崩溃
崩溃描述： Supported orientations has no common orientation with the application, and [UdeskBaseNavigationViewController shouldAutorotate] is returning YES
解决方案：屏幕旋转问题 在目标Controller增加 shouldAutorotate { return no }

3.dyld: Library not loaded崩溃，现象描述打开app直接崩溃<img width="433" height="235" alt="截屏2025-11-03 18 23 52" src="https://github.com/user-attachments/assets/79da14c3-6528-4370-9e8b-a1bf3fe80cc8" /> 
解决步骤：打开app崩溃几次——去手机的隐私分析中查看崩溃记录可查看有问题的动态库
# ios开发工具![IMG_0003](https://github.com/user-attachments/assets/3e0dbba8-db35-447e-ad47-5a9f6fd9ac8c)

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

1.png转webp：https://anywebp.com/png-to-webp
