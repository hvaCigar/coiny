# USERS
Все манипуляции с пользователями

## GET /users/
Получить данные о всех пользователях. Можно получить информацию о пользователе с определенными параметрами: username, email или id. Могут быть введены как все сразу, так и по отдельности (только username или только email).


### Request
Без параметров

#### Query
    {
    }

### Response
Ответ отправит массив со всеми пользователями

#### Code
200 OK

#### Body

    [
        {
            uuid: "01234567-89ab-cdef-0123-456789abcdef",
            email: "blabla@bla.bla",
            username: "sample_username",
            created_at: "2012-01-01T12:00:00Z",
            updated_at: "2012-01-02T12:00:00Z",
        },
        {
            uuid: "01234567-8etc-cdef-0123-456789abcdef",
            email: "blabla@bla2.bla",
            username: "sample_username2",
            created_at: "2012-01-01T12:00:00Z",
            updated_at: "2012-01-02T12:00:00Z",
        }
    ]

### Request
Запрос с параметрами. Поле содержит массив с данными. Все поля необязательны для заполнения. 

#### Query
    {
        // username: optional
        username: [
            "sample_username", 
            "sample_username2"
        ],
        // email: optional
        email: [
            "blabla@bla.bla",
            "blabla@bla2.bla",
        ]
        uuid: [
            "01234567-89ab-cdef-0123-456789abcdef",
            "01234567-8etc-cdef-0123-456789abcdef",
        ]
    }
    
### Response
Ответ от сервера отправит массив данных со всеми пользователями, которые попадают под запрос. 

#### Code
200 OK

#### Body
    [
        {
            uuid: "01234567-89ab-cdef-0123-456789abcdef",
            email: "blabla@bla.bla",
            username: "sample_username",
            created_at: "2012-01-01T12:00:00Z",
            updated_at: "2012-01-02T12:00:00Z",
        },
        {
            uuid: "01234567-8etc-cdef-0123-456789abcdef",
            email: "blabla@bla2.bla",
            username: "sample_username2",
            created_at: "2012-01-01T12:00:00Z",
            updated_at: "2012-01-02T12:00:00Z",
        }
    ]
    
## Ошибки запросов в GET /users/    
    
### Response 
Ничего не найдено по тем параметрам, которые были отправлены

#### Code
404 Not Found 

#### Body
    {
        error: true,
        message: "Ничего не найдено по запросу",
    }

### Response
Доступ запрещен, клиент не может получать данные о пользователях

#### Code
403 Forbidden

#### Body 
    {
        error: true
        message: "Доступ запрещен"
    }

## POST /users/
Создать пользователя

### Request
#### Body

    {
        email: "blabla@bla.bla",
        password: "123456"
    }

### Response
#### Code
201 Created

#### Body

    {
        email: "blabla@bla.bla",
        password: "123456",
        createdAt: 131535254242,
        uuid: "71818181-89ab-cdef-0123-456789abcdef"
    }

### PUT /users/71818181-89ab-cdef-0123-456789abcdef
Обновить информацию о пользователе (частично)

### Request
#### Headers

    Authorization: 548ee277bf0bb00001c55db4

#### Body

    {
        password: "qwerty"
    }

### Response
#### Code

    200 OK

#### Body

    {
        email: "blabla@bla.bla",
        password: "qwerty",
        createdAt: 131535254242,
        updatedAt: 248492749274,
        uuid: "71818181-89ab-cdef-0123-456789abcdef"
    }

### DELETE /users/71818181-89ab-cdef-0123-456789abcdef
Удалить пользователя

### Request
#### Headers

    Authorization: 548ee277bf0bb00001c55db4

### Response
#### Code

    204 No Content