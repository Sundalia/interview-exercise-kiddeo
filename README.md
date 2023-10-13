# interview-exercise-kiddeo

## Оглавление
1. [Оценочные параметры](#оценочные-параметры)
2. [Термины](#термины)
3. [Задача](#задача)
4. [Описание](#описание)
5. [Рабочая область](#рабочая-область)
6. [Ключ](#ключ)
7. [Набор начальных параметров страницы](#набор-начальных-параметров-страницы)
8. [Конечные точки (API endpoints)](#конечные-точки-api-endpoints)

## Оценочные параметры
Это тестовое задание составлено с целью оценить:

- Ваше умение читать документацию и разбираться с первого взгляда неясными программными интерфейсами. (в данном случае Google Maps API) Google maps является не самым лёгким инструментом, потому что есть много нюансов, политика использования и затруднительная в восприятии картина, которая загоняет проект в определённые рамки. Для своего развития можете почитать про другие подобные инструменты, сравнить их, их требования, подумать какие лучше будут подходить под стратегию развития каких проектов и стратегию выхода на какие рынки.
- Проверить ваш опыт в среде разработки по показателям уровня креативности, который сформировался по прошествии других проектов.
- Умение раскладывать всё по полочкам. Мы надеемся, что работа будет выполнена аккуратно и ответственно.
- Умение работать с данными. (перебирать, модернизировать, использовать)

Вы можете перейти на пошаговое выполнение этого задания. [Щёлк!](#)

Вы можете посмотреть дополнительные задачи, которые помогут увеличить верхний предел вилки данной вакансии. [Щёлк!](#)

## Термины
- **Страница «добавления метки»** - страница, на которую мы попадаем при нажатии на кнопку добавить метку. Данная страница состоит из одного input и одного select элемента. В первый заносится адрес. Во втором мы выбираем помещение из заранее сгенерированного списка, который мы также получаем каждый раз при переходе на эту страницу. Параметры для отображения списка в виде options внутри select будут выглядеть следующим образом. [Щёлк!](#)
- **После нажатия кнопки сохранить, поле из input[name=’address’] попадает в геокодер, который заполняет hidden поля после двух предыдущих. Это долгота и широта. (x и y)** 

## Задача

### Что должно быть:

1. **Google карта.** При загрузке страницы должен быть preloader на карте, она должна получать метки из базы данных (база данных уже есть в проекте и настроена) и загружать их на карту.
   - Вам понадобится использовать Google Maps JavaScript API для отображения карты;
   - Для preloader’а, вы можете использовать CSS или JavaScript анимации, чтобы показать пользователю, что карта загружается.

2. **Список всех помещений (параметры уже в переменной при запуске страницы).** При клике на помещение, оно показывается на карте и происходит zoom;
3. **Строка поиска продуктов на карте.** Поиск поддерживает как ввод адреса, так и ввод названия помещения;
4. **Кнопка добавить метку;**
5. **При нажатии на метку на карте выводится маленькое модальное окно в нижнем правом углу карты с информацией:**
   - Картинка;
   - Название продукта с права замочек;
   - Адрес помещения справа замочек.
   - Кнопка редактировать, которая убирает замочек и позволяет изменить данные, а на картинке появляется крестик (добавить возможность загрузить и удалить фотографию без запроса);
   Замочки для примера. Можете сделать так, можете придумать что-нибудь своё.
6. **Checkbox или что-то подобное для удаления сразу нескольких меток на карте;**
7. **На странице «добавления метки» будет input, при вводе address в который, срабатывает geocoder, который заносит координаты в hidden input;**
8. **Вторым полем на странице «добавления метки» является select с выбором определённого продукта. Select choices получаются запросом к API
9. **Ниже на странице «добавления метки» кнопка сохранить.**

## Описание

Перед тестируемым стоит задача разработать скажем некий интерфейс, который в теории мог бы применяться в панели администратора или мог бы стать частью личных кабинетов пользователей какого-нибудь приложения. В рамках тестового мы с вами попробуем реализовать секцию в админ панели. Чтобы разобраться куда писать код перейдите в раздел рабочая область.

Любые моменты в интерфейсе можете придумать сами, в разделе «Задача» они для примера, чтобы показать требуемый функционал.

Логика работы такая:
- Хотим найти что-нибудь на карте, используем для этого поиск или список имеющихся помещений с метками;
- Если помещение не было найдено при поиске, нажимаем кнопку создать метку и переходим на другую страницу, где имеем 3 поля - 2 видимых и 1 скрытое.
- Заполняем видимые поля, автоподбором через геокодер подтягиваются долгота и широта, которые попадают в невидимое поле coordinates;
- Нажимаем кнопку сохранить.
- Также должна быть возможность редактировать данные по метке и удалить их.

Следовательно, начинаем со страницы "создания меток". Получаем список параметров для этой подзадачи и реализуем форму создания метки помещения. Форма отправляется по URL адресу.

Так, создание метки работает, теперь создаём основную страницу и начинаем с карты. Для реализации карты нам понадобится Google Maps JavaScript API. Чтобы получить ключ [щелкните сюда](https://developers.google.com/maps/gmp-get-started).

Также обращаемся к API для получения параметров, после чего нам приходят наши созданные метки и мы перебираем метки и расставляем их по карте. Метки можно сделать обычными, без кастомизации. В базе данных уже есть 5 помещений, используя которые, можно создать метки.

Затем верстаем информационное окно и ковыряемся в параметрах карты, чтобы реализовать zoom при нажатии на список помещений или при поиске, которые нам тоже нужно сделать.

## Рабочая область

Для того, чтобы начать выполнение тестового вам потребуется:
- Зайти на [Git](https://github.com/Weorano/interview-exercise-kiddeo) и сделать fork проекта.
- Сделать git clone проекта, установить Python, выбрать interpreter и создать виртуальное окружение.
- В консоли выполнить следующие команды:
  - `pip install -r requirements.txt` – установка библиотек;
  - `python manage.py runserver` – запуск сервера.
- Зайти в админ панель (/admin в URL) с логином `admin` и паролем `admin`. Секция `maps` представляет вашу рабочую область. База данных применится автоматически (используется SQLite), поэтому вам будут доступны 5 тестовых продуктов с картинками.
- Перейти в `templates/admin/maps.html` – это пустая страница в административной панели, на которой вам предстоит работать. На ней будет сама карта.
- Для работы с Google используйте ключ (если не работает, отправьте сообщение менеджеру).

## Наборы начальных параметров страницы

При загрузке страницы мы получаем список `map_parameters`:

![image](https://github.com/Weorano/interview-exercise-kiddeo/assets/50415153/b5bfdb40-91bf-4670-8fbf-004296f5bf9d)

1. `geo_placemark_coordinates: [x, y]`;
2. `product_name`;
3. `product_address`;
4. `product_image`.

Имейте в виду, что в списке `geo_placemark_coordinates` находятся в строковом формате. Сделано это для быстрого запуска проекта (чтобы не использовать Array).

При переходе на страницу "добавления метки" мы отправляем запрос к API и получаем список `products_choices`:

1. `id: `;
2. `name: "Название помещения"`.

Нужно будет приложить `id` в `product_id` для создания метки.

## Конечные точки (API endpoints)

![image](https://github.com/Weorano/interview-exercise-kiddeo/assets/50415153/da70c184-633a-422e-9d71-860907f6a7a8)

![image](https://github.com/Weorano/interview-exercise-kiddeo/assets/50415153/dc768d56-86e9-4f84-be80-219d6190e2c5)

![image](https://github.com/Weorano/interview-exercise-kiddeo/assets/50415153/9a9179cc-a50e-41a0-ae8b-602f96635958)

- `Coordinates` – array(size=2)
