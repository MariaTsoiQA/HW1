**Документация по запуску REST API**

Postman-коллекция: https://drive.google.com/file/d/1ciao66NH-8RC-WTbiZXiW6uCHJRn--ON/view?usp=sharing

В Variables коллекции указаны значения переменных:
   
   "owner" - владелец учетной записи репозитория,
   
   "repo" - имя репозитория,
   
   "API_key" - API-ключ учетной запаси

   "number" - номер задачи (добавляется автоматически при создании задачи)

   

**ЗАПРОСЫ:**
   
**1. СОЗДАНИЕ задачи**

  Используем метод **POST**

  **URL**: https://api.github.com/repos/{{owner}}/{{repo}}/issues

 **Headers** содержит:

  Accept - application/vnd.github+json

  Authorization - Bearer {{API_key}}

  Вводим в **Body** JSON

  {
    "title":"Issue 1",
    "body":"Something went wrong",
    "assignees":["MariaTsoiQA"],
    "labels": ["bug"]
  }

где "title" это название задачи, "body" описание задачи, "assignees" имя ученой записи того кому мы адресуем эту задачу,  "labels" тип задачи (в нашем случае баг).

Отправляем запрос и получаем в ответе "Body", в котором указан номером нашей задачи (номер задачи сохраняется в переменую для последующего использования). Статус код 201.

**2. ПРОСМОТР созданной задачи**

  Используем метод **GET**

  **URL**: https://api.github.com/repos/{{owner}}/{{repo}}/issues/{{number}} , где number - номер нашей созданной задачи.

 **Headers** содержит:

  Accept - application/vnd.github+json

  Authorization - Bearer {{API_key}}

Отправляем запрос и получаем в ответе "Body" всю информацию о созданной задаче. Статус код 200.

**3. ПРОСМОТР всего списка задач в репозитории**

  Используем метод **GET**

  **URL**: https://api.github.com/repos/{{owner}}/{{repo}}/issues

 **Headers** содержит:

  Accept - application/vnd.github+json

  Authorization - Bearer {{API_key}}

Отправляем запрос и получаем в ответе "Body" все задачи которые имеются в данном репозитории. Статус код 200.

**4. ПЕРЕИМЕНОВАТЬ созданную задачу**

  Используем метод **PATCH**

  **URL**: https://api.github.com/repos/{{owner}}/{{repo}}/issues/{{number}}

 **Headers** содержит:

  Accept - application/vnd.github+json

  Authorization - Bearer {{API_key}}

  Вводим в **Body** JSON, где указываем в "title" новое название задачи

  {"title":"Issue 2"}

Отправляем запрос и получаем в ответе "Body", в котором видим новое название задачи. Статус код 200.

**ВАЖНО !!!**
**Мы не можем полностью удалить созданную задучу из репозитория при помощи основных методов без использования мутаций. Но мы можем ограничить доступ к нашей задачи заблокировав ее, чтобы никто не мог ею воспользоваться. Так же, в случае необходимости, мы можем разблокировать эту задачу.**

**5. ЗАБЛОКИРОВАТЬ созданную задачу**

  Используем метод **PUT**

  **URL**: https://api.github.com/repos/{{owner}}/{{repo}}/issues/{{number}}/lock

 **Headers** содержит:

  Accept - application/vnd.github+json

  Authorization - Bearer {{API_key}}

  Вводим в **Body** JSON, где указываем в "lock_reason"  причину блокировки

 {"lock_reason":"off-topic"}

Отправляем запрос и получаем в ответ пустое "Body". Статус код 204.

**5. РАЗБЛОКИРОВАТЬ задачу**

  Используем метод **DELETE**

  **URL**: https://api.github.com/repos/{{owner}}/{{repo}}/issues/{{number}}/lock

 **Headers** содержит:

  Accept - application/vnd.github+json

  Authorization - Bearer {{API_key}}

Отправляем запрос и получаем в ответ пустое "Body". Статус код 204.

