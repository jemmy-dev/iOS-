# iOS-开发问题集锦
1.Operation not permitted
解决方案：在项目Build Settings中搜索"user script sandboxing"选项，将其值改为"No"可解决相关权限问题
2.UIApplicationInvalidInterfaceOrientation崩溃
崩溃描述： Supported orientations has no common orientation with the application, and [UdeskBaseNavigationViewController shouldAutorotate] is returning YES
解决方案：屏幕旋转问题 在目标Controller增加 shouldAutorotate { return no }


# ios开发工具
1.png转webp：https://anywebp.com/png-to-webp
