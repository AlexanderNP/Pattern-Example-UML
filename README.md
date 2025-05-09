# MVC

## Паттерн MVC - это скорее не паттерн, а архитектурный стиль. 
* M - model, это некая сущность которая отвечает за данные, бизнес логику
* V - View, это представление, т.е. некоторый видимый результат, который получает данные из Model через Controller.
* C - Controller, можно сказать что это мозг, который отвечает за распределение процесса между представление и моделью.
* ***Т.е. Model ничего не знает про V и C, также как и View ничего не знает про M***

## Пример на беке
Исходя из моего опыта взаимодействия с Node js сервером и написания серверных приложений, все стараются ПРИДЕРЖИВАТЬСЯ или даже сами того не понимая используего данный архитектурный стиль.

В данном случае:

* Model - база данных
* View - какое-либо визуальное отображение с сервера (шаблонизация)
* Controller - обработчики запрос-ответ, которые как-раз перенеправляют и взаимодействуют с View и Model

## Пример на фронте
Как все соверменные/популярные фреймворки/библиотеки (React, Vue, ...) закладывают в реализацию данный архитектурный стиль.

Рассмотрим как пример логику логина пользователя.

![MVC UML](MVC.png)

# Observer

## Паттерн Observer - это паттерн который позволяет объектам оповещать другие объекты об изменениях своего состояния.

## Observer включает в себя:

* Издатель - это основной класс, который служит неким слушателем, т.е. если было выполнено какое-то соыбытие, он уведомит всех своих подписчиков, которые были подписаны на данное событие. 
  - Обычно в нем содержится 4 метода:
    - Метод для подписки
    - Метод для отписки
    - Метод для уведомления
    - Метод который выполняет какую-то общую бизнес логику для всех компонентов, перед уведомлением.
  - И 2 поля:
    - Список подписчиков привязанных к конкретном событию (eventType)
    - Состояние издателя
* Наблюдатели - это классы, которые подписываются на событие и выполняют свою внутренную логику.
  - Метод для выполнения конкретной зоны отвественности наблюдателя.

***Важно, чтобы наблюдатели имплеминитировали один и тот же интерфейс, для того чтобы в классе издателе, можно было вызывать его не привязываясь к конкретному классу (структурная типизация)***

## Рассмотрим на примере проекта "Корпоративная база знаний":

Есть категории, которые интересны определенным пользователям, например "Пути развития в компании". Определенные пользователи хотят видеть уведомление, и также, например, увелечение счетчика уведомлений у себя (это и будет общая бизнес логика у издателя для всех пользотвалей, кто подписался на данное события), когда в данную категорию попадает новая статья.

После добавления статьи, пользователи оценивают её (у каждого пользователя единый интерфейс, т.е. все должны как-минимум иметь метод оценки статьи)

Т.е. в данном случае ***издаталем является категория***, а ***наблюдатели эта все пользователи***, которые ***подписаны на событие добавление новой статить в категорию***.

![Observer UML](Pattern-Observer.png)

# Singleton

## Паттерн Singleton - это паттерн, который реализаует 1-ну глобальную сущность, например при создании экземпляра базы данных, данная петтерн гарантирурет, что при попытке создать ещё один новый экземпляр, он всегда будет возвращать один и тот же instance.

Одним из примеров на фронте, это State Manager Redux, который как раз закладывает в себя принцип единого истончика данных. 

В целом это удобно, но с масштабирование приложения начнут возникать проблемы, т.к. этот источник данных начнет БЕЗМЕРНО разрастаться с добавлением новой бизнес-логики.
Т.е. сама концепция паттерна ***не позволяет делать архитктуру модульной***, делить её на независящие друг от друга слои.

## Рассмотрим также на примере проекта "Корпоративная база знаний", когда его можно использовать:

Например сущность "Избранные категории", это 1-на глобальная сущность на все приложение.
При попытке создать ещё один экземпляр, всегда будет возращаться один и тотже, с данными которые пользователь добавил.

![Observer UML](Singleton.png)
