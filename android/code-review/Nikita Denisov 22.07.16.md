# Общие замечания

- Использвание `@NonNull` и `@Nullable` аннотаций для предотвращения NPE

- Удалять лишнюю документацию при кодогенерации 
```
/**
 * @return The success
 */
public boolean isSuccess() {
    return success;
}
```
- Следовать единому стилю именования ресурсов

- Для получения профита от MVP избавиться от android-зависимостей в presenter и view

# Git

- Не хранить в Git служебные файлы, так как они несут ненужную смысловую нагрузку, помещать их в игнор

- Изучить правильный стиль именования коммитов и веток

- Определить для актульной версии проекта отдельную ветку и сливать в нее последние изменения. Для тестирования каких-либо фич и иных целей создавать отдельную ветку

# Оформления кода

- Условные операторы обязательно должны иметь фигурные скобки

- Неправильное именование констант, наличие `final` предполагает использование `static`

- Для исключения дублирования кода вспомогательные методы вынести в отдельный класс Util

# Замечения к коду

- `findViewById()` дорогостоящая операция, чтобы постоянно не дергать ее для `ListView` адаптера использовать `ViewHolder`

- Для облегчения java-кода часть UI-методов вынести в xml

- Стили применять через `style`, а не `android:theme`

- Неправильное использование наследования стилей для view-элементов

- Использование атрибута `android:drawableRight`
