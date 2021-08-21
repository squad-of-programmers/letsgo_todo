# lets go! todo list, api doc

### Начало работы (для запуска проекта нужна нода 14 версии)
1. делаем git clone + скопированный путь в терминале, где открыта нужная папка.
![git clone](http://images.vfl.ru/ii/1604317442/3803189d/32158503.png)

2. В терминале открываем папку server и вводим команду **npm i** - для того, чтобы все зависимости установились, а далее **node seed.js** и **node server.js**

3. В терминале открываем папку client и вводим команду **yarn** - для того, чтобы все зависимости установились, а далее **yarn start**
В этот момент в браузере откроется наше приложение
![main page](http://images.vfl.ru/ii/1629503197/3db55eb3/35571894.jpg)

### Данные для заполнения табличной части приходят из базы данных
![redux](http://images.vfl.ru/ii/1604318264/ed4f6ab5/32158739.png)

### Внешний вид личного кабинета сотрудника департамента туризма
![lk department](http://images.vfl.ru/ii/1629503606/43ed8fc9/35571903.jpg)

### Страница из личного кабинета сотрудника департамента туризма, на которой можно ознакомиться с блогерами, информация о которых имеется в базе данных
![bloggers from data base](http://images.vfl.ru/ii/1629503817/22f95a63/35571909.jpg)

### Создание нового мероприятия / турах сотрудником департамента туризма
![create event](http://images.vfl.ru/ii/1629504267/0c1a6075/35571917.jpg)

### Информация о мероприятиях, которую видит сотрудник департамента туризма
![events](http://images.vfl.ru/ii/1629504187/bb4a56a5/35571915.jpg)

### Детальная информация о мероприятии, которую видит сотрудник департамента туризма
![detail info event](http://images.vfl.ru/ii/1629503980/ddf3a8eb/35571912.jpg)

### Форма регистрации блогера, представителя СМИ
![blogger registry](http://images.vfl.ru/ii/1629519627/190600c7/35572362.png)

### Внешний вид личного кабинета блогера, представителя СМИ
![lk blogger](http://images.vfl.ru/ii/1629503696/8fd9f087/35571905.jpg)

### Имеется возможность **сортировки** данных в столбцах с *локация*, *количество подписчиков*, *количество посещенных мероприятий*. Для этого нужно нажать на сам заголовок
![sort](http://images.vfl.ru/ii/1604319169/a9effc19/32158941.png)

### В работе использован react-router
![route](http://images.vfl.ru/ii/1604320591/ddef4a18/32159243.png)

### Информация о сотрудниках хранится в MongoBD
![db](http://images.vfl.ru/ii/1629503275/5c86cda2/35571895.png)




## todo items:
* [ ] Просмотр списка блогеров
    * [ ] Добавление блогера в группу
    * [ ] Удаление блогера из поиска
  
* [ ] тур
    * [ ] Создание с указанием даты? проведения
    * [ ] Удаление
    * [ ] Изменение
    * [ ] Добавление места/пункта в тур с указанием времени
    * [ ] Удаление места/пункта из тура
* [ ] место/пункт/event
    * [ ] Создание 
    * [ ] Удаление  
    * [ ] Изменение
    

* [ ] Создание новой группы блогеров
  ```txt
  Предлагаю сделать так:
  на старнице просмотра/отбора новых блогеров 
  можно будет помечать галочкой нужные поля людей и потом нажать 
  на кнопку сверху 'добавить в группу' - это выпадающее меню где
  можно посмотреть все группы и если нужной ещё нет то в том же списке
  есть кнопка `add new`
  ```
* [ ] Просмотр группы блогеров
* [ ] Написание сообщения и рассылка приглашений группе (на email)
* [ ] Отправка приглашения на email одному блогеру

* [ ] Страница с новостями и ближайшими турами


* [ ] добавление парсера c соцсетей
    * [ ] facebook
    * [ ] instagram

#
## questions:
* date/dates/range in tours?
* PUT or PATCH? or Post?


Почему django?
Я вижу у Django следующие преймущества:
* Простота и обширный набор функций, позволяющая с высокой скоростью создать приложение
* Достаточно высокая производительность для приложения с невысокой нагрузкой на бд(основные пользователи сайта - администраторы мин. туризма опр. города)

#
## api:
* [ ] GET: http://host/bloggers/ - получение списка блогеров
```json5
{
  "bloggers": [
    {
      "id": 12345,
      "name": "Ivanov Ivan",
      "email": "some@email.com",
      "avatar": "media/avatars/...", // "" if there is no avatar
      "gender": 'm'|'w',
      "last_date_invitation": 19932451325,  
      // думаю, если блогер уже в туре - присылать его не будем
      // также не будем его показывать, если он уже был приглашён в этом месяце
      "social_networks": {
        "facebook": "link",
        "instagram": "link",
        // ... There will be more fields in the future
      }
      
    },
    // ...
  ]
}  
```
  

* [ ] DELETE: http://host/bloggers/{blogger_id}/ - удаление блогера из поиска полностью
* [ ] PUT: http://host/groups/{group_id}/bloggers/{blogger_id}/ - добавление блогера в группу
* [ ] POST: http://host/groups/{group_id}/send_invitation/ - отправка письма группе блогеров 
```json5
{
  "title": "some text",
  "body": "some text",
  "recipients": [123, 1214, 11], // ids of bloggers
  
}
```


* [ ] POST: http://host/bloggers/{blogger_id}/send_invitation/ - отправка письма одному блогеру
```json5
{
  "title": "some text",
  "body": "some text",
  "recipients": [123, 1214, 11], // ids of bloggers
  
}
```


* [ ] GET: http://host/events - получить места для посещения блогерами
```json5
// получаем следующее
{
  "points": [
    {
      "id": 1234,
      "title": "museum",
      "description": "some text",
      "address": "Samara, some street 3",
    },
    // ...
  ]
}
```
* [ ] POST: http://host/groups/ - создание группы с выбранными блогерами
```json5
{
  "bloggers": [123, 1214, 11], // ids of bloggers
}
```


* [ ] GET: http://host/groups/{group_id} - получение группы со списком блогеров
```json5
{
  "bloggers": [123, 1214, 11], // ids of bloggers
}
```


* [ ] POST: http://host/tours/ - Создание турка
```json5
{
  "title": "some text",
  "description": "some text",
  "date": "??????", // ????????
  "events": [
    {
      "title": "some text",
      "description": "some text",
      "address": "Samara, some street 3",
      "time": 19943523452345, 
    },
    // ...
  ]
}
```

* [ ] DELETE: http://host/tours/ - Удаление тура
* [ ] PUT: http://host/tours/{tour_id} - Изменение данных тура
```json5
{
  "title": "some text",
  "description": "some text",
  "date": ""
}
```
* [ ] PUT: http://host/tours/{tour_id}/events/{event_id} - Добавление места/пункта в тур с указанием времени
* [ ] DELETE: http://host/tours/{tour_id}/events/{event_id} - Открепление места/пункта из тура

* [ ] POST: http://host/events/ - Создание even
```json5
{
  "title": "some text",
  "description": "some text",
  "address": "Samara, some street 3",
  "time": 19943523452345, 
}
```
* [ ] DELETE: http://host/events/{event_id} - Удаление event
* [ ] PUT: http://host/events/{event_id} - Изменение event
```json5
{
  "title": "some text",
  "description": "some text",
  "address": "Samara, some street 3",
  "time": 19943523452345, 
}
```
