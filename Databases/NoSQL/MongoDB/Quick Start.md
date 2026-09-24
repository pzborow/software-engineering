# Quick Start


## Połączenie via `mongo` lokalnie
```.bash
pzborow@sv36 [~]# mongo --host mongo
MongoDB shell version: 3.0.7
connecting to: mongo:27017/test
> use pzborow_test
switched to db pzborow_test
> db.auth("pzborow_test", "tGpC0Jg61S6COVlcQnOuXZSu1")
1
>
```

Hasło `tGpC0Jg61S6COVlcQnOuXZSu1`

## Utworzenie nowego użytkownika
```
db.createUser({
user: "joe",
pwd: "alamakota",
roles: [ "readWrite" ],
passwordDigestor:"server"
})
```

kasowanie usera joe z bazy `db.dropUser("joe")`

## Połączenie via `mongsh`
` mongosh "mongodb://mongo-598989.vipserv.org:27017/pzborow_test" --username joe`

## Połączenie via `compass`

Compass to narzędzie GUI do łącznie się z MongoDB

## Inne

[Samouczek](https://www.w3schools.com/mongodb/mongodb_charts.php)
[Dokukumentacja](https://www.mongodb.com/docs/manual/)

[Docker mongo](https://hub.docker.com/_/mongo)
[Docker mongo expres](https://hub.docker.com/_/mongo-express)