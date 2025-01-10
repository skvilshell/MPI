# диаграмма последовательностей
## Авторизация
```uml
@startuml

actor User as u
participant FrontEnd as fe
participant BackEnd as be
database db

u -> fe : "Ввод логина и пароля"
fe -> fe: Валидация
fe -> be: /login
be -> db: findUser()
db -> be: {token}
be -> fe: 201:{token}
fe -> fe: auth(token)
fe -> u: "Успешный вход"

@enduml
```
## Регистрация
```uml
@startuml

actor User as u
participant FrontEnd as fe
participant BackEnd as be
database db

u -> fe : "Ввод логина и пароля"
fe -> fe: Валидация
fe -> be: /register
be -> db: userByEmail()
db -> be: null
be -> db: addUser()
db -> be: {token}
be -> fe: 201:{token}
fe -> fe: auth(token)
fe -> u: "Успешный вход"

@enduml
```
## экспорт
```uml
@startuml

participant BoNalog as n
actor Moderator as m
participant FrontEnd as fe
participant BackEnd as be
database db

m -> n: выгрузка отчета
m -> fe: загрузка
fe -> fe: валидация
fe -> be: /order
be -> db: checkOrder()
db -> be: null
be -> db: saveOrder()
db -> be: {order}
be -> fe: 201:{order}
fe -> m: "показать успех"

@enduml
```
# Пользовательские сценарии
```uml
@startuml

actor User as u
actor Moderator as m

rectangle App {
  usecase "Авторизация" as UC1
  usecase "Экспорт" as UC2
  usecase "Поиск" as UC3
  usecase "Просмотр отчета" as UC4
}

u --> UC1
m --> UC1
m --> UC2
u --> UC3
u --> UC4

@enduml
```
# 

# Классы
```
@startuml

class Orginzation {
+  String inn
-  String name
-  String date_create
}

class User {
+  String id
-  String name
-  String surname
-  Orginzation inn
  Role role
  
}

enum Role {
  Client
  Moderator
}

class Order {
#  String id
#  User moderator_id
#  Date date_create
  ...
}

User *-- Orginzation
Order *-- Orginzation
Order *-- User
Role --* User

@enduml
```

