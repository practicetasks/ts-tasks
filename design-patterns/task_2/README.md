# Задача

Перед вами класс `Client`, который описывает клиента сети ресторанов. У клиента есть имя — name и метод — `makeOrder`,
он помогает делать заказы.

Клиент, который сделал пять заказов, считается постоянным и получает скидку 10% на все последующие заказы. Чтобы считать
заказы и вовремя сообщать клиентам радостную новость, напишем прокси-класс `ClientProxy`. В коде приведена его заготовка
и комментариями отмечены места, в которых вы должны дописать код.

Ваши задачи

* Реализовать логику подсчёта заказов;
* Как только клиент сделал пятый заказ, вывести в консоль сообщение: «{имя}, поздравляем! Теперь вы наш постоянный
  клиент и получаете на скидку 10%!». Вместо слова «имя» подставьте имя клиента.

```ts
interface IClient {
    name: string;
    makeOrder(meal: string): void;
}

class Client implements IClient {
    constructor(public name: string) {}

    makeOrder(meal: string) {
        console.log(`${this.name} заказал ${meal}`);
    }
}

class ClientProxy implements IClient {
    private client: IClient;

    /* TODO: Объявите приватный счетчик заказов */

    constructor(client: IClient) {
        this.client = client;

        /* TODO: Инициализируйте счётчик нулём */
    }

    get name() {
        return this.client.name;
    }

    set name(value: string) {
        this.client.name = value;
    }

    makeOrder(meal: string) {
        /* TODO: Реализуйте метод makeOrder:
            1. Выполните исходный makeOrder
            2. Увеличьте счётчик
            3. Если клиент сделал 5 заказов, выведите строку:
                "{имя}, поздравляем! Теперь вы наш постоянный клиент и получаете скидку 10%!"
         */
    }
}

const client = new ClientProxy(new Client('Адиль'));

client.makeOrder('салат Оливье');
client.makeOrder('шашлык');
client.makeOrder('пюре с котлетой');
client.makeOrder('салат Оливье');
client.makeOrder('борщ');
```