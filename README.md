# FUTabBarController
*Custom FUTabBarController


### CocoaPods

  1. Add `pod 'FUTabBarController', '~> 1.0.0'` to your Podfile.

  2. Run `pod install` or `pod update`.

  3. 创建UITabBarController自定义类 继承FUTabBarController
  4. 具体实现可以看demo`Home->MainTabBarController.m`


#父类中提供的方法
## <a id="initialize"></a>
```objc
//添加中心按钮：模态...（子类调用）
- (void)addCenterItemWithIcon:(NSString *)iconName selectedIcon:(NSString *)selectedIconName title:(NSString *)title offset:(BOOL)offset clickBlock:(ClickBlock)block;
/**
*  初始化一个子控制器
*
*  @param childVc               需要初始化的子控制器
*  @param navigationController  导航控制器
*  @param title                 标题
*  @param imageName             图标
*  @param selectedImageName     选中的图标
*  @param offset                是否凸出（YES：按钮向上凸出）
*/
- (UIViewController *)setupChildViewController:(UIViewController *)childVc navigationController:(Class)navigationController title:(NSString *)title imageName:(NSString *)imageName selectedImageName:(NSString *)selectedImageName offset:(BOOL)offset;
@end
```


# 子类中给viewControllers赋值就可以了
## <a id="setup"></a>
```objc
- (void) setUpChildControllers
{
//动态
UIStoryboard *trendsStB = [UIStoryboard storyboardWithName:@"TrendsViewController" bundle:nil];
TrendsViewController *trendsVC = [trendsStB instantiateViewControllerWithIdentifier:@"TrendsViewController"];
UIViewController *trendsNVC = [self setupChildViewController:trendsVC navigationController:[MainNavController class] title:@"动态" imageName:@"trends_nomal.png" selectedImageName:@"trends_select.png" offset:NO];

//名片
UIStoryboard *callingCardStB = [UIStoryboard storyboardWithName:@"CallingCardViewController" bundle:nil];
CallingCardViewController *callingCardVC = [callingCardStB instantiateViewControllerWithIdentifier:@"CallingCardViewController"];
UIViewController *callingCardNVC = [self setupChildViewController:callingCardVC navigationController:[MainNavController class] title:@"名片" imageName:@"callingCard_nomal.png" selectedImageName:@"callingCard_select.png" offset:NO];

//宝信
UIStoryboard *baoXinStB = [UIStoryboard storyboardWithName:@"BaoXunViewController" bundle:nil];
BaoXunViewController *baoXinVC = [baoXinStB instantiateViewControllerWithIdentifier:@"BaoXunViewController"];
UIViewController *baoXinNVC = [self setupChildViewController:baoXinVC navigationController:[MainNavController class] title:@"宝信" imageName:@"baoxin_nomal.png" selectedImageName:@"baoxin_select.png" offset:NO];

//我的
UIStoryboard *mineStB = [UIStoryboard storyboardWithName:@"MineViewController" bundle:nil];
MineViewController *mineVC = [mineStB instantiateViewControllerWithIdentifier:@"MineViewController"];
UIViewController *mineNVC = [self setupChildViewController:mineVC navigationController:[MainNavController class] title:@"我的" imageName:@"mine_nomal.png" selectedImageName:@"mine_select.png" offset:NO];

self.viewControllers = @[trendsNVC, callingCardNVC, baoXinNVC, mineNVC];

//添加中心按钮（只适用于中心按钮模态弹出）
//offset:是否凸出
__weak typeof(self) weakSelf = self;
[self addCenterItemWithIcon:@"search_nomal" selectedIcon:@"search_nomal" title:@"搜索" offset:YES clickBlock:^{
UIStoryboard *board = [UIStoryboard storyboardWithName:@"SearchViewController" bundle:nil];
SearchViewController *searchVC= [board instantiateViewControllerWithIdentifier:@"SearchViewController"];
UIViewController *searchNVC = [weakSelf setupChildViewController:searchVC navigationController:[MainNavController class] title:@"我的" imageName:@"" selectedImageName:@"" offset:NO];

[weakSelf presentViewController:searchNVC animated:YES completion:nil];
}];


}

@end
```

### 有标题 + 凸出
<img src="http://p1.bqimg.com/1949/115761d623008b5a.png" width="30%" height="30%">
### 无标题 + 凸出
<img src="http://p1.bqimg.com/1949/fa8b0df53bf311f9.png" width="30%" height="30%">
### 有标题 + 不凸出
<img src="http://p1.bqimg.com/1949/d940e83b61a32eed.png" width="30%" height="30%">
### 无标题 + 不凸出
<img src="http://p1.bqimg.com/1949/0603d24e7556c4ba.png" width="30%" height="30%">
