# USERS
Все манипуляции с пользователями

## GET /users/
Получить данные о всех пользователях. 


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
            created_at: "2012-01-01T12:00:00Z",
            updated_at: "2012-01-02T12:00:00Z",
        },
        {
            uuid: "01234567-8etc-cdef-0123-456789abcdef",
            email: "blabla@bla2.bla",
            created_at: "2012-01-01T12:00:00Z",
            updated_at: "2012-01-02T12:00:00Z",
        }
    ]


## GET /users/?email=blabla@bla@.bla&uuid=01234567-89ab-cdef-0123-456789abcdef
Можно получить информацию о пользователе с определенными параметрами: email или uuid. Могут быть введены как все сразу, так и по отдельности (только uuid или только email).

### Request
Запрос с параметрами. Поле содержит массив с данными. Все поля необязательны для заполнения. 

#### Query
    {
        // email: optional
        email: [
            "blabla@bla.bla",
            "blabla@bla2.bla",
        ]
        // uuid: optional
        uuid: [
            "01234567-89ab-cdef-0123-456789abcdef"
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
            createdAt: "2012-01-01T12:00:00Z",
            updatedAt: "2012-01-02T12:00:00Z",
        },
        {
            uuid: "01234567-8etc-cdef-0123-456789abcdef",
            email: "blabla@bla2.bla",
            createdAt: "2012-01-01T12:00:00Z",
            updatedAt: "2012-01-02T12:00:00Z",
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


## POST /users/
Создать пользователя

### Request
#### Body

    {
        email: "blabla@bla.bla",
        password: "123456",
    }

### Response
#### Code
    201 Created

#### Body

    {
        email: "blabla@bla.bla",
        password: "123456",
        createdAt: "2012-01-01T12:00:00Z",
        uuid: "71818181-89ab-cdef-0123-456789abcdef"
    }

## Ошибки запросов в POST /users/    
    
### Response 
Не может быть создан пользователь с такими данными

#### Code
    406 Not Acceptable

#### Body
    {
        error: true,
        message: "Пользователь с такими данными уже существует",
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
    
## Общие ошибки    
### Response
Доступ запрещен, клиент не может получать данные

#### Code
403 Forbidden

#### Body 
    {
        error: true
        message: "Доступ запрещен"
    }
