# Android. Мобильное приложение

  - Android Studio 2022.1.1
  - Kotlin 1.8.10
  - Android SDK 32
  - Gradle 7.6 (управление зависимостями)
  - Material 2 (создание пользовательского интерфейса)
  - Room 2.5.0 (работа с базой данных)
  - Kotlinx.Serialization 1.4.1 (сериализация JSON)
  - Retrofit 2.9.0 (сетевое взаимодействие)
  - Dagger 2.45 (внедрение зависимостей)
  - Kotlin Coroutines 1.6.4 (асинхронная работа)
  - Использование архитектурного паттерна MVVM
  - Присутствие трех основных слоев приложения: данных, бизнес-логики и пользовательского интерфейса

1. Слой данных (datasource)
   - База данных
      - Созданы отдельные модели (Entity) для таблиц базы данных
      - Имя модели как ИмяEntity (Например, UserEntity)
      - Реализованы CRUD-операции
   - Сетевой сервис
      - Созданы отдельные модели (Dto) с сериализатором
      - Имя модели как ИмяDto (Например, UserDto)
2. Слой бизнес-логики (domain)
   - Созданы отдельные модели (Domain)
   - Имя модели как Имя (Например, User)
   - Реализованы мапперы для Dto<->Domain, Entity<->Domain
   - Мапперы в виде [функций расширения](https://kotlinlang.org/docs/extensions.html)
   - Реализован репозиторий для работы с базой данных
   - Реализован репозиторий для работы с сетевым сервисом
3. Внедрение зависимостей (DI)

Проверяется правильность получения и сохранения данных можно с помощью логирования

### Реализация слоя пользовательского интерфейса

1. Реализовать слой пользовательского интерфейса (presentation)
   - Главный экран
      - Кнопка обновления информации об объектах:
         - По нажатии на кнопку происходит получение данных об объектах с сервера
         - Операция получения данных с сервера выполняется асинхронно и не блокировать главный поток
         - При ошибке получения данных с сервера показается всплывающее уведомление на экране
         - Данные, полученные с сервера, сохраняются в базу данных
         - Операция сохранения данных с сервера выполняется асинхронно и не блокирует главный поток
      - Список с краткой информацией об объектах:
         - Данные для отображения берутся из базы данных
         - Операция получения информации из базы данных выполняется асинхронно и не блокирует главный поток
         - Элемент списка содержит несколько текстовых полей, а также картинку
         - При нажатии на элемент списка происходит переход на экран с подробностями об объекте
      - Поддерживаться горизонтальная и вертикальная ориентация устройства
   - Экран с подробностями об объекте
      - Детальная информация об объекте:
         - Отображается полная информация об объекте
         - Данные загружаются из сети в базу данных
         - Операция загрузки данных из сети в базу данных выполняется асинхронно и не блокирует главный поток
         - Данные для отображения получаю из базы данных
         - Операция получения информации из базы данных выполняется асинхронно и не блокирует главный поток
         - Обеспечивается возможность прокрутки отображаемых данных, если не все содержимое помещается на экране
         - Поддерживается горизонтальная и вертикальная ориентация устройства
   - Созданы отдельные модели (ViewData)
   - Имя модели формируется как ИмяViewData (Например, UserViewData)
   - Реализованы мапперы ViewData<->Domain
   - Мапперы оформлены в виде [функции расширения](https://kotlinlang.org/docs/extensions.html)
2. Обеспечена связь между слоем пользовательского интерфейса и слоем бизнес-логики

