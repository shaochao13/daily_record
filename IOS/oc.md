1. UIButton 实现左字右图       
默认情况下，是左图右字，需要把它们的位置掉换一下。
```
-(void) viewDidLayoutSubviews{
    [super viewDidLayoutSubviews];   
    //让button 实现 右图左字
    UIImage * image = [UIImage imageNamed:@"18up"];
    [self.minuteBtn setImage:image forState:UIControlStateNormal];
    [self.minuteBtn setImage:[UIImage imageNamed:@"18down"] forState:UIControlStateSelected];
    [self.minuteBtn setImageEdgeInsets:UIEdgeInsetsMake(0, self.minuteBtn.titleLabel.frame.size.width, 0, 0)];
    [self.minuteBtn setTitleEdgeInsets:UIEdgeInsetsMake(0, -image.size.width, 0, 0)]; 
}
```

2. 获得应用的版本号（Version／Build）  
    获得应用的Verison号：  

    ```Objective-c
    [[[NSBundle mainBundle] infoDictionary] objectForKey:@"CFBundleShortVersionString"]

    ```
    或：  

    ```
    [[NSBundle mainBundle] objectForInfoDictionaryKey:@"CFBundleShortVersionString"];
    ```

    获得build号:   

    ```
    [[[NSBundle mainBundle] infoDictionary] objectForKey:@"CFBundleVersion"];
    ```