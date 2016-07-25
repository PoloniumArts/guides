# Общие замечания

 - respond_to do |format| в api это лишнее

 - Отдельное пространство имён для API (api/v1), сделать каталоги. Чтобы было удобнее потом создавать следующие версии API

 - Я бы сделал locale файл c текстами ошибок на случай повторного использования одного и того же сообщения.

# Замечения к коду

 - valid_date_time повторяется в концерне и контроллере

 - total_counts в ResultTestsController я бы перенес модель и сделал чтобы она возвращала значение а не создавала переменную экземпляра. И почему protected а не  private?

 - CalendarActionsController. if 0.3 < distance константу стоит перенести в модель

 - можно сделать scope для Body в BodiesController#index

 - (@alarm_clocks.start_time - @alarm_clocks.end_time).abs < (@alarm_clocks.total_cigarettes - @alarm_clocks.want_cigarettes) * 60 такую обьемную логику не стоит хранить в контроллере

 - В CalendarActions методы для времени я бы перенес в helper или модель

 - timetable_string в модели  WorkingDay я бы переименовал в update_timetable_string так как метод не возвращает значение а обновляет (Изначально подумал что это get-метод). Переменные экземпляра в функции я бы сделал обычными, они только запутывают. Аналогично User.change_avatar_by_rating

В общем только одно большое пожелание. Различную логику, алгоритмы, запросы связанные с предметной областью стоит выносить в модель. Принцип Fat Model, Skinny Controler.
