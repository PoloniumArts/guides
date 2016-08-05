# themes_controller.rb
 - Предложу свою версию метода find_theme в которой отсутствуют совсем не обязательные проверки и код имхо компактнее смотрится
    ```ruby
    def find_theme
      id = params[:theme_id]
      id ||= params[:id]
      @theme = current_user.themes.find_by(id: id)
      unless @theme
        render json: { error: 'Доступ запрещен' }, status: 403
      end
    end
    ```
 - условия в age_range_from_params я бы переписал через тернарный оператор
 - в модели Theme status это скоуп ради скоупа. Я думаю было бы лучше вложить в него ещё и логику.
      ```ruby
      scope :status, -> (s) do
        if s != 'archive'
          where(status: ['disabled', 'active'])
        else
          where(status: 'archive')
        end
      end
      ```
    тогда в контроллере можно будет просто написать
    ```ruby
    @themes = current_user.themes.status(params[:status])
    ```
 - В методах add_sources и send_retro_complete_info я думаю нужно изменить find_by на find или дописать проверку на существование темы. Иначе где то дальше возможно будет падение
# reports_controller.rb
 - Пути к изображениям, отчётам, pdf думаю стоит определять в конфигах
 - в методах где render json вызывается один раз нет нужды делать return
 - save_png имхо стоит перенести в helper
 - метод status стоит переписать, так как сейчас он работает неэффективно, потому что для каждого отчета генерируется update запрос. Cтоит использовать метод update_all. Он сгенерирует один запрос на обновление всех отчётов
