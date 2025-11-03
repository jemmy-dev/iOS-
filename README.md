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

1.png转webp：https://anywebp.com/png-to-webp
