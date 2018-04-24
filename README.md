# FullscreenPopGesture
iOS 全屏返回手势。使用黑魔法，在UINavigationController的分类或者UIViewController控制是否启用手势。轮子的创造大部分借鉴sunnyxx的[FDFullscreenPopGesture](https://github.com/forkingdog/FDFullscreenPopGesture)。


# 使用方法

- 导入头文件FullscreenPopGesture.h

- 全局手势开关

``` 
self.navigationController.popGestureRecognizer.enabled = YES;//默认开启
```

- 控制器属性开关 

``` objc
self.interactivePopDisabled = NO;//当前控制器是否开启手势,默认NO
self.prefersNavigationBarHidden = NO;//导航条是否隐藏，默认NO
```

# 手势冲突

当控制器的view包含UIScrollView,全局手势会与UIScrollView默认的手势冲突。解决思路：判断全局手势，并且滑动到最左侧，则启用多重手机，否则不启用多重手势。

``` objc
- (BOOL)gestureRecognizer:(UIGestureRecognizer *)gestureRecognizer shouldRecognizeSimultaneouslyWithGestureRecognizer:(UIGestureRecognizer *)otherGestureRecognizer {
    
    if (self.contentOffset.x <= 0) {
        if ([otherGestureRecognizer.delegate isKindOfClass:NSClassFromString(@"UINavigationController")]) {
            return YES;
        }
    }
    return NO;
}

``` 

# 截图

![snapshot](./screenshots.gif)
