# USERS
Все манипуляции с пользователями

## GET /users/
Получить данные о всех пользователях

### Response
#### Code
200 OK

#### Body

    [
        {
            uuid: "01234567-89ab-cdef-0123-456789abcdef",
            email: "blabla@bla.bla"
        },
        {
            uuid: "71818181-89ab-cdef-0123-456789abcdef",
            email: "second@one.com"
        }
    ]

## GET /users/
Получить информацию о пользователе с определенными параметрами

### Request
#### Query
    {
        login: "sample_username",
        email: "blabla@bla.bla",
        id: "12345"
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