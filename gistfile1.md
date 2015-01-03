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

## GET /users/
Получить информацию о пользователе с определенными параметрами: username, email или id. Могут быть введены как все сразу, так и по отдельности (только username или только email).

### Request
#### Query
    {
        username: [
            "sample_username", 
            "sample_username2"
        ],
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
    
### Code
#### 

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