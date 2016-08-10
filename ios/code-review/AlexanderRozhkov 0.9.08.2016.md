
1. Неиспользуемые файлы в проекте
	* UIDevice+PoloniumArts, UIView+PoloniumArts
1. Modern Objective-C: Edit-> Convert-> To Modern Objective-C syntax
	* Вместо [NSNumber numberWithFloat:M_PI  isOpened / 2.0] лучше @(M_PI  isOpened / 2.0) 
	* Вместо dictionaryWithObjectsAndKeys -> @{}
1. AZRatingTop50TableViewCell
	* Не уверен, что этот код должен вызываться каждый раз при обновлении ячейки
``` 	self.avatarImageView.layer.cornerRadius  = self.avatarImageView.width / 2.0;
```
``` 	self.avatarImageView.layer.masksToBounds = YES;
```
1. Не думаю, что это хороший код:
``` self.detailsLabel.preferredMaxLayoutWidth = [UIApplication sharedApplication].keyWindow.bounds.size.width - 60.0;
```
 [https://www.objc.io/issues/3-views/advanced-auto-layout-toolbox/]()

1. Pods
	* pod 'UITableView+FDTemplateLayoutCell' - C iOS 8 есть Self-SIzing Cells
	* SWTableViewCell - iOS 8+???
	* Fabric, Crashlytics лучше поставить через поды.
1. Для чего используется класс AZBaseBarButton?
1. AZAPIClient+EventsAndPlaces - много параметров в методах
1. NSDate+PoloniumArts - лучше использовать либо DateTools, либо новые методы для работы с временем, добавленные в iOS 8.
1. Tell, don't ask: AZPersonalCalendarMainDataTableViewCell
1. Синусы и косинусы в AZGroupMarker
1. AZAvatarTableViewController - дублирование методов dataSource, delegate
1. Очень много логики в контроллерах, завязка на подклассы.