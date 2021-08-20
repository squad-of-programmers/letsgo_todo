# lets go! todo list, api doc
### features:
* [x] Просмотр списка блогеров
    * [x] Добавление блогера в группу
    * [x] Удаление блогера из поиска
  
* [x] тур
    * [x] Создание с указанием даты? проведения
    * [ ] Удаление
    * [ ] Изменение
    * [ ] Добавление места/пункта в тур с указанием времени
    * [ ] Удаление места/пункта из тура
* [ ] место/пункт
    * [ ] Создание 
    * [ ] Удаление  
    * [ ] Изменение  
    

* [x] Создание новой группы блогеров
  ```txt
  Предлагаю сделать так:
  на старнице просмотра/отбора новых блогеров 
  можно будет помечать галочкой нужные поля людей и потом нажать 
  на кнопку сверху 'добавить в группу' - это выпадающее меню где
  можно посмотреть все группы и если нужной ещё нет то в том же списке
  есть кнопка `add new`
  ```
* [x] Просмотр группы 
* [x] Написание сообщения и рассылка приглашений группе (на email)
* [x] Отправка приглашения на email одному блогеру

### questions:
...

### api:
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
        "facebook": "linkstr",
        "instagram": "linkstr",
        // ... There is will be more fields in the future
      }
      
    },
    // ...
  ]
}  
```
  

* [ ] DELETE: http://host/bloggers/{blogger_id} - удаление блогера из поиска полностью
* [ ] PATCH: http://host/bloggers/{blogger_id}/{group_id} - добавление блогера в группу
* [ ] POST: http://host/groups/{group_id}/send_invitation - отправка письма группе блогеров 
```json5
{
  "body": "some text",
  "recipients": [123, 1214, 11], // ids of bloggers
  
}
```


* [ ] POST: http://host/bloggers/{blogger_id}/send_invitation - отправка письма одному блогеру
```json5
{
  "body": "some text",
  "recipients": [123, 1214, 11], // ids of bloggers
  
}
```


* [ ] GET: http://host/locations - получить места пригодные для посещения блогеров
```json5
// получаем следующее
{
  "points": [
    {
      "id": 1234,
      "title": "museum", // например, музей
      "description": "some text",
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
      "title",
      "description",
      "adress",
      "time", 
    },
    // ...
  ]
}
```