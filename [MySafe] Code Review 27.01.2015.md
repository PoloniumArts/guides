## Общие замечания
* Убрать TestFlight SDK из проекта, он уже не поддерживается
* Убрать ворнинги из проекта: "Automatic Preferred Max Layout Width is not available on iOS versions prior to 8.0" и тп. [ссылка](http://www.objc.io/issue-3/advanced-auto-layout-toolbox.html)
* Убрать ворнинги статического анализатора.
* Убрать ворнинги из логов(в частности с констрейнтами)
* В проекте не должно быть неиспользуемых ресурсов и файлов, все ненужное должно быть удалено, например, файлы в группе "Category".
* Неиспользуемый, задокументированный код тоже нужно убрать.

## Замечания по коду
* При создании объектов Foundation следует использовать [литералы](http://www.bignerdranch.com/blog/objective-c-literals-part-1/)
* При задании фреймов иногда удобнее воспользоваться функциями из [CGGeometry](http://nshipster.com/cggeometry/). Также не следует забывать про [View Layout Process](https://developer.apple.com/library/ios/featuredarticles/ViewControllerPGforiPhoneOS/AdoptingaFull-ScreenLayout/AdoptingaFull-ScreenLayout.html#//apple_ref/doc/uid/TP40007457-CH13-SW2)
* В проекте есть категория UIFont+Additions, туда следует помещать часто используемые шрифты.  
Например, вместо `[UIFont fontWithName:@"AvenirNext-Regular" size:16.0f]`, лучше сделать `[UIFont avenirNextWithSize:16.f]`, чтобы не писать каждый раз названия шрифтов вручную.
* Для анимации лучше использовать блоки(`MSVMainMenuViewController`)

```
 	- (IBAction)closeButtonPressed:(id)sender {
 	    self.containerView.alpha = 1;
 	    [UIView beginAnimations:nil context:nil];
 	    [UIView setAnimationDuration:2];
 	    [UIView setAnimationDelegate:self];
 	    self.containerView.alpha = 0;
 	    [UIView commitAnimations];
 	}
```
* Код создания контроллеров лучше помещать внутрь контроллера, например:

```
MSVSignInViewController *controller = [MSVSignInViewController signInViewController];
...
+ (instancetype)signInViewController {
	    UIStoryboard *storyboard = [UIStoryboard storyboardWithName:@"Main" bundle:nil];// если параметр bundle nil, то сториборд ищется в mainBundle, см. доку.
    return [storyboard instantiateViewControllerWithIdentifier:NSStringFromClass(self)];
}
```
* `MSVReservationViewController`(для KVO лучше использовать [KVOController](https://github.com/facebook/KVOController))
* Для чего используется этот код? Он используется во многих местах, в крайнем случае его можно поместить в категорию.

```
    UIGraphicsBeginImageContext(self.view.frame.size);
    [[UIImage imageNamed:@"bg"] drawInRect:self.view.bounds];
    UIImage *image = UIGraphicsGetImageFromCurrentImageContext();
    UIGraphicsEndImageContext();
    
    self.view.backgroundColor = [UIColor colorWithPatternImage:image];
```

* Имена уведомлений лучше делать константами, т.е. вместо `@"characterButtonPressed"` лучше сделать `NSString *const MSVCharacterButtonPressedNotification = "MSVCharacterButtonPressedNotification"`. Но в данном случае уведомление о нажатии кнопки во вьюхе лучше делать через делегата.
* С этим кодом явно нужно что-то делать(**MSVKeyboardViewController**), в других местах тоже есть подобное.

```
    if ([[UIScreen mainScreen ] bounds].size.height == 480) {
        [view setFrame:CGRectMake(0, 220, 320, 300)];
    } else if ([[UIScreen mainScreen ] bounds].size.height == 568.0f) {
        [view setFrame:CGRectMake(0, 300, 320, 300)];
    } else {
        [view setFrame:CGRectMake(20, 400, 400, 300)];
    }
```

* Не следует использовать приватное API, в этом случае приложение скорее всего будет отклонено Apple.

```
- (void)changeDatePickerColor {
    [self.timePicker setValue:[UIColor whiteColor] forKeyPath:@"textColor"];
    
    SEL selector = NSSelectorFromString(@"setHighlightsToday:");
    NSInvocation *invocation = [NSInvocation invocationWithMethodSignature:[UIDatePicker instanceMethodSignatureForSelector:selector]];
    BOOL no = NO;
    [invocation setSelector:selector];
    [invocation setArgument:&no atIndex:2];
    [invocation invokeWithTarget:self.timePicker];
}

... 

{
    UIApplication *app = [UIApplication sharedApplication];
    [app performSelector:@selector(suspend)];
}
```
* `MSVStoreHousePhotoViewController`
* Вместо рисования в drawRect: в большинстве случаев лучше использовать CAShapeLayer, так как это быстрее.