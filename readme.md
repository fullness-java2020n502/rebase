```
@startuml
skinparam shadowing false
hide fields
hide methods

package presentation{
    class UserController
}
package application{
    class UserService
    class UserDTO
}
package domain.model{
    class User
    class UserId
    interface UserRepository
}
package infrastructure{
    class UserRepositoryJpa implements UserRepository
    class UserRepositoryMybatis
    class UserRepositoryHogeApi
    class UserJpaModel
}
package H2_DB <<Database>>{
    entity "User_Table" as user
}
package 外部サービス <<Database>>{
    entity "顧客データ" as customer
}
UserRepositoryJpa -> UserJpaModel : create
UserController -> UserService : call
UserService --> UserRepository : call
UserRepository -> User : create
User o- UserId
UserRepositoryJpa --> user : SQL
UserRepositoryHogeApi --> customer : REST API
@enduml

@startuml

package domain.model{
    class User
    class UserId
    class Name
    class Password
    interface UserRepository
}

User o--> UserId: has-a
User o--> Name: has-a
User o--> Password: has-a
UserRepository -> User: 永続化

package infrastructure{
    class UserRepositoryDummy implements UserRepository
    class UserRepositoryJpa implements UserRepository
}

@enduml

```
