# Задача

Попробуйте реализовать Facade самостоятельно.

Есть сервис для работы с данными пользователей — он знает их имена и город, умеет находить пользователя в списке по
`id`:

```ts
interface User {
    id: string,
    name: string,
    city: string,
}

class UserService {
    private users: User[] = [
        {id: '2061', name: 'Роберт', city: 'Астана'},
        {id: '7494', name: 'Тимур', city: 'Алматы'},
        {id: '5864', name: 'Асылхан', city: 'Шымкент'},
        {id: '9300', name: 'Илья', city: 'Караганда'},
        {id: '3756', name: 'Бексултан', city: 'Актобе'},
    ];

    getCurrentUser(id: string) {
        return this.users.find(user => user.id === id);
    }
}
```

Также есть сервис, который знает, в каком регионе находится каждый город.

```ts
interface City {
    name: string,
    region: string,
}

class GeoService {
    private cities: City[] = [
        {name: 'Астана', region: 'Акмолинская область'},
        {name: 'Алматы', region: 'Алматинская область'},
        {name: 'Шымкент', region: 'Туркестанская область'},
        {name: 'Караганда', region: 'Карагандинская область'},
        {name: 'Актобе', region: 'Актюбинская область'},
    ];

    getCity(cityName: string) {
        return this.cities.find(city => city.name === cityName);
    }
}
```

Наша цель — написать фасад, который будет использовать оба сервиса. Одна из его задач —находить регион пользователя с
нужным `id`.

Класс Facade уже определён. Вам осталось реализовать в нём метод `getUserRegion`. Он должен:

* принимать `id` пользователя (строка);
* возвращать регион, в котором находится пользователь.

Используйте для этого экземпляры классов `UserService` и `GeoService`!

```ts
class Facade {
    constructor(private users: UserService, private geo: GeoService) {
    }

    /* реализуйте метод getUserRegion */
}

const facade = new Facade(new UserService(), new GeoService());

console.log(
    facade.getUserRegion('5864')
);
```