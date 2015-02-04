* Весь неиспользуемый код нужно убрать, для хранения истории есть Git.
* Код инициализации вьюх следует располагать либо в designated initializer класса, либо в awakeFromNib, установку фреймов в layoutSubviews(перед этим не забыв вызвать super).
* **NGPartnersCardTableViewCell** 
 
```
	if (![self.titlePercents.textColor isEqual:dataColor]) {
		self.titlePercents.textColor          = dataColor;
		self.titlePercentSymbol.textColor     = dataColor;
		self.title.textColor                  = dataColor;
		self.discountLabel.textColor          = dataColor;
		self.mainPercents.textColor           = dataColor;
		self.mainPercentsSymbol.textColor     = dataColor;
		self.lookAtRestaurantsLabel.textColor = dataColor;
	}
```
Более короткое решение объединить лейблы в IBOutletCollection и вызвать `[self.labels makeObjectsPerformSelector:@selector(setTextColor:) withObject:dataColor]`

* **NGAroundViewController** - работа с координатами точек(лучше использовать встроенные функции MapKit, либо GoogleMapsSDK, нужно покурить доку).