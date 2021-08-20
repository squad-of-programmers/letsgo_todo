# lets go! todo list, api doc

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