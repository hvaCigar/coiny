# USERS
Все манипуляции с пользователями

## GET /users/
Получить данные о всех пользователях. 


### Request
#### Headers

    Authorization: 548ee277bf0bb00001c55db4

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

### Request
Запрос с параметрами. Поле содержит массив с данными. Можно получить информацию о пользователе с определенными параметрами: email или uuid. Могут быть введены как все сразу, так и по отдельности (только uuid или только email).

#### Headers

    Authorization: 548ee277bf0bb00001c55db4

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
        {
            key: 'uuid',
            message: "Пользователи с запрошенным UUID не существуют",
            uuid: "01234567-8etc-cdef-0123-456789abcdef" // uuid несуществующих пользователей
        },
        {
            key: 'email',
            message: "Пользователи с запрошенным email не существуют",
            email: "wrong@mail.err" // email несуществующих пользователей
        }
    }

### Response 
Пользователь не может получать данные, у него нет доступа к получению данных об именно этих пользователях. Обычный пользователь может получить данные только о себе, а администратор - о всех. Если при GET-запросе на /users/ вылезает 403, то пользователь не является администратором и пробует получить не свои даные.

#### Code
    403 Forbidden

#### Body
    {
        {
            key: 'Rules',
            message: "Права не позволяют вам смотреть информацию не о себе"
        }
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
    400 Bad Request

#### Body
    {
        {
            key: 'email',
            message: "Пользователь с такой почтой уже существует"
        },
        {
            key: 'email',
            message: "Некорректный формат почты"
        },
        {
            key: 'password',
            message: "Пароль слишком простой"
        }
    }

### PUT /users/71818181-89ab-cdef-0123-456789abcdef
Обновить информацию о пользователе (частично)

### Request
#### Headers

    Authorization: 548ee277bf0bb00001c55db4

#### Body

    {
        password: "qwerty",
        email: "newbla@bla.bla"
    }

### Response
#### Code

    200 OK

#### Body

    {
        email: "newbla@bla.bla",
        password: "qwerty",
        createdAt: 131535254242,
        updatedAt: 248492749274,
        uuid: "71818181-89ab-cdef-0123-456789abcdef"
    }
    
    
## Ошибки запросов в PUT /users/    
    
### Response 
Новые данные некорректны

#### Code
    400 Bad Request

#### Body
    {
        {
            key: 'email',
            message: "Пользователь с такой почтой уже существует"
        },
        {
            key: 'email',
            message: "Некорректный формат почты"
        },
        {
            key: 'password',
            message: "Пароль слишком простой"
        }
    }

### Response 
Недостаточно прав для редактирования профиля. Всплывает когда человек пытается отредактировать не свой профиль, не являясь админом.

#### Code
    403 Forbidden

#### Body
    {
        {
            key: 'Rules',
            message: "Вы пытаетесь отредактировать не свой профиль, но не являетесь администратором, вам отказано в доступе"
        }
    }

### DELETE /users/71818181-89ab-cdef-0123-456789abcdef
Удалить пользователя

### Request
#### Headers

    Authorization: 548ee277bf0bb00001c55db4

### Response
#### Code

    204 No Content
    

## Ошибки запросов в DELETE /users/       
### Response 
Недостаточно прав для удаления профиля. Всплывает когда человек пытается удалить не свой профиль, не являясь админом.

#### Code
    403 Forbidden

#### Body
    {
        {
            key: 'Rules',
            message: "Вы пытаетесь удалить не свой профиль, но не являетесь администратором, вам отказано в доступе"
        }
    }

# SPENDING
Все манипуляции с расходами

## GET /spending/
Получить данные о всех своих расходах. 


### Request
#### Headers
    
    Authorization: 548ee277bf0bb00001c55db4

#### Query
    {
    }

### Response
Ответ отправит массив со всеми расходами

#### Code
    200 OK

#### Body

    [
        {
            value: 12000,
            unit: "RUB",
            created_at: "2012-01-01T12:00:00Z",
            updated_at: "2012-01-02T12:00:00Z",
        },
        {
            value: 300,
            unit: "USD",
            created_at: "2012-01-01T12:00:00Z",
            updated_at: "2012-01-02T12:00:00Z",
        }
    ]

### Request
Запрос с параметрами. Поле содержит массив с данными. Можно получить информацию о расходах с определенными параметры. Параметры описаны в Query. Все условия поиска комбинируются логическим И, то есть результат выдается только на те расходы, которые полностью совпали по всем параметрам.

#### Headers

    Authorization: 548ee277bf0bb00001c55db4
    // Отсюда будет взят uuid пользователя, расходы которого можно посмотреть

#### Query
    {
        // unit: optional
        // Массив с нужными валютами
        unit: [
            "RUB",
            "USD",
            "EUR"
        ],
        // value: optional
        value: {
            // fixed найдет все расходы с конкретными значениями из массива
            // Если используется поле fixed, то не должно быть полей max/min, и наоборот
            fixed: [ 
                15000,
                60000
            ]
            // min устанавливает нижнюю границу значений
            min: 30000,
            // max устанавливает максимальную границу значений
            max: 60000
        },
        date: {
            // fixed найдет все расходы с конкретными датами из массива
            // Если используется поле fixed, то не должно быть полей max/min, и наоборот
            fixed: [
                '2012-01-01T12:00:00Z',
                '2012-01-02T12:00:00Z'
            ],
            // min устанавливает нижнюю границу даты
            min: '2010-01-01T12:00:00Z',
            // max устанавливает максимальную границу даты
            max: '2016-01-01T12:00:00Z'
        }
    }
    
### Response
Ответ от сервера отправит массив данных со всеми расходами, которые попадают под запрос. 

#### Code
    200 OK

#### Body
    [
        {
            value: 12000,
            unit: "RUB",
            created_at: "2012-01-01T12:00:00Z",
            updated_at: "2012-01-02T12:00:00Z",
        },
        {
            value: 300,
            unit: "USD",
            created_at: "2012-01-01T12:00:00Z",
            updated_at: "2012-01-02T12:00:00Z",
        }
    ]
    
## Ошибки запросов в GET /spending/    

### Response 
Запрос на поиск составлен неверно

#### Code
    400 Bad Request 

#### Body
    {
        {
            key: 'value',
            message: "Нельзя использовать одновременно поле fixed и min/max в value"
        },
        {
            key: 'value',
            message: 'Граница min должна быть меньше max'
        },
        {
            key: 'value',
            message: 'Значения должны быть integer, неверный формат данных'
        },
        {
            key: 'date',
            message: "Нельзя использовать одновременно поле fixed и min/max в date"
        },
                {
            key: 'date',
            message: 'Граница min должна быть меньше max'
        },
        {
            key: 'date',
            message: 'Значения должны быть формата "2012-01-01T12:00:00Z", неверный формат данных'
        },
        {
            key: 'unit',
            message: 'Валюта набрана неверно или отсутствует в списке валют'
        }
    }

    
### Response 
Ничего не найдено по тем параметрам, которые были отправлены

#### Code
    404 Not Found 

#### Body
    {
        {
            key: 'Search',
            message: "Ничего не найдено с указанными параметрами поиска"
        }
    }

### Response 
Не авторизован

#### Code
    403 Forbidden

#### Body
    {
        {
            key: 'Authorization',
            message: "Вы не зашли ни под каким пользователем, получать данные о расходах не можете"
        }
    }


## POST /spending/
Создать пользователя

### Request

#### Headers

    Authorization: 548ee277bf0bb00001c55db4
    // Отсюда будет взят uuid пользователя, расходы которого нужно создать


#### Body

    {
        value: 10000,
        unit: "RUB",
    }

### Response
#### Code
    201 Created

#### Body

    {
        value: 10000,
        unit: "RUB",
        createdAt: "2012-01-01T12:00:00Z",
        uuid: "71818181-89ab-cdef-0123-456789abcdef" // uuid расхода, а не пользователя
    }

## Ошибки запросов в POST /spending/    
    
### Response 
Неверный формат входных данных

#### Code
    400 Bad Request

#### Body
    {
        {
            key: 'unit',
            message: 'Валюта набрана неверно или отсутствует в списке валют'
        },
        {
            key: 'value',
            message: 'Значение должно быть integer, неверный формат значения расходов'
        }
    }
    
### Response 
Не авторизован

#### Code
    403 Forbidden

#### Body
    {
        {
            key: 'Authorization',
            message: "Вы не зашли ни под каким пользователем, создавать расходы не можете"
        }
    }

### PUT /spending/71818181-89ab-cdef-0123-456789abcdef
Обновить информацию о расходе с его uuid

### Request
#### Headers

    Authorization: 548ee277bf0bb00001c55db4

#### Body

    {
        value: 12000,
        unit: "RUB"
    }

### Response
#### Code

    200 OK

#### Body


    {
        value: 10000,
        unit: "RUB",
        createdAt: "2012-01-01T12:00:00Z",
        uuid: "71818181-89ab-cdef-0123-456789abcdef" // uuid расхода, а не пользователя
    }
    
    
## Ошибки запросов в PUT /spending/    
    
### Response 
Новые данные некорректны

#### Code
    400 Bad Request

#### Body
    {
        {
            key: 'unit',
            message: 'Валюта набрана неверно или отсутствует в списке валют'
        },
        {
            key: 'value',
            message: 'Значение должно быть integer, неверный формат значения расходов'
        }
    }

### Response 
Недостаточно прав для редактирования расхода. Это значит, что uuid расхода не привязан к пользователю, который пытается его редактировать

#### Code
    403 Forbidden

#### Body
    {
        {
            key: 'Rules',
            message: "Вы не можете редактировать чужие расходы, не будучи администратором"
        }
    }

### Response 
Не авторизован

#### Code
    403 Forbidden

#### Body
    {
        {
            key: 'Authorization',
            message: "Вы не зашли ни под каким пользователем, создавать расходы не можете"
        }
    }

### DELETE /spendinig/71818181-89ab-cdef-0123-456789abcdef
Удалить расход

### Request
#### Headers

    Authorization: 548ee277bf0bb00001c55db4

### Response
#### Code

    204 No Content
    

## Ошибки запросов в DELETE /spending/   

### Response 
Недостаточно прав для удаления расхода. Это значит, что uuid расхода не привязан к пользователю, который пытается его удалить

#### Code
    403 Forbidden

#### Body
    {
        {
            key: 'Rules',
            message: "Вы не можете удалять чужие расходы, не будучи администратором"
        }
    }

### Response 
Не авторизован

#### Code
    403 Forbidden

#### Body
    {
        {
            key: 'Authorization',
            message: "Вы не зашли ни под каким пользователем, удалять расходы не можете"
        }
    }
    
У доходов все тоже самое, как и у расходов, только /spending/ заменено на /incoming/
