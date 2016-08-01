1. Git OMG - проект не собирается, отсутствуют файлы 
Был баг гита, файлы добавил. Собирается.
2. Dependencies FXBlurView - UIVisualEffect 
О: уже нет нужды в этой либе. MZFormSheetController - MZFormSheetPresentationController 
O: заменил XCDYouTubeKit 
O: ненужна, используется более легковестная либа от гугла  «youtube-ios-player-helper»
3. В сторибордах не заданы констрейнты  Прочитать Auto Layout Guide, WWDC 14,15
О: Забыл установить кое где констрейнты, исправил.
4. Копипаст в VTBAPIClient
O: Исправил
5. VTBEducationCollectionViewCell - преобразование строк в перечисления
O: Исправил, добавил перечисления везде где нужно.
6. Копипаст с рублями
O: Исправил, вынес в модели.
7. IBOutletCollection
O: В местах где много однотипных элементов исправил на outlet collection
8. VTBDocumentAddViewController, VTBDocumentAddViewController - Обработка данных должна находиться в моделях
О: Вынес обработку в отдельный класс, но нужно чуть доделать, в свободное время доделаю.