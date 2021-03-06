# Тут вы найдете сайт, который поможет вам правильно сварить кофе
#### Команда разработчиков: Осипян Арсен, Шарипов Тимур, ФАЛТ МФТИ

## О проекте
Данный проект написан с использованием Flask и SQL. На данный момент предоставляет функциональность для двух типов пользователей - модераторов и обычных пользователей.

А `Chicco di caffe` - это с итальянского `кофейное зерно`.

## Запуск сервера
Основной файл - `chicco_di_caffe.py`.
Для `windows cmd`:
```python
$ set FLASK_APP=chicco_di_caffe.py
$ flask run
```

Для `unix shell`:
```python
$ export FLASK_APP=chicco_di_caffe.py
$ flask run
```

## Структура бэкенда
Работа с базой данных реализована через SQLAlchemy, используя 3 основные модели таблицы - `User`(пользователь), `Recipe`(рецепт кофе) и `Sort`(соответственно, сорт кофе).
Структуру непосредственно самих моделей смотрите в файле `app/models.py`.

Вся логика работы с URL-запросами и обработкой форм представлена в файле `app/routes.py`. Реализована начальная защита, как то использование декоратора `@login_required`, не позволяющий анонимному пользователю просматривать страницы и совершать какие-то действия. Обратите внимание, что некоторые URL являются фиктивными, после выполнения каких-то действий сразу же происходит `redirect` на другую страницу. 
Представлены страницы пользователя, личный кабинет, главная страница, страницы для каждого рецепта и сорта кофе, а так же страница управления базой данных для администраторов.

Формы ввода данных от пользователя описаны в файле `app/forms.py`. Там реализованы форма регистрации пользователя, форма входа пользователя, форма добавления рецепта, форма добавления сорта кофе, а так же формы для `редактирования` уже существующих рецептов, сортов и форма `изменения пароля`.
Все формы имеют валидаторы и уведомляют пользователей об ошибке ввода.

Реализованы также шаблоны для страницы `404` и `500`. В дальнейшем планируется добавить опцию уведомления админов на email при 500-той ошибке сервера.

Весь сайт написан с использованием шаблонов, подшаблонов и их наследования, что позволило избежать дублирования кода. Помимо этого, для фронтенда использовалась библиотека `bootstrap`, предоставляющая готовые дизайны. 

Формой добавления(редактирования) рецепта могут пользоваться только администраторы и авторы рецепта. Формой добавления(редактирования) сорта могут воспользоваться только администраторы. 

Формой изменения пароля может воспользоваться любой, пароль сменится, только если вы верно ввели старый.

Помимо этого, у админов есть доступ к панели управления базой данных, позволяющей видеть все элементы базы, иметь к ним прямой доступ и возможность удалить любой элемент из базы.

Добавлена `flavicon`-иконка для сайта

На странице каждого пользователя отображаются рецепты, предложенные им

При удалении пользователя из БД удаляются все связанные с ним рецепты

При удалении сорта кофе так же удаляются все связанные с ним рецепты

На страницах админов рядом с ником отображается смайлик в черных очках:sunglasses:!

Чтобы проверить весь функционал, используйте логин `Tim` и пароль `1`.

## Что в будущем:
+ email-уведомления админам при ошибке сервера
+ Добавить уникальные картинки к разным сортам кофе
