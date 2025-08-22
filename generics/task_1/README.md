# Задача

1. Создайте класс `Order`, который будет содержать:
    - `product: Product`
    - `quantity: number`
2. Создайте класс `OrderStorage` на основе `BaseStorage`.
3. Реализуйте метод `getTotalValue()`, который будет возвращать суммарную стоимость всех заказов.

```ts
class Product {
    title: string;
    price: number;

    constructor(title: string, price: number) {
        this.title = title;
        this.price = price;
    }
}

class BaseStorage<T> {
    items: T[] = [];

    addItem(item: T): void {
        this.items.push(item);
    }

    removeItem(item: T): void {
        this.items = this.items.filter(i => i !== item);
    }

    getItem(index: number): T {
        return this.items[index];
    }
}

class ProductStorage extends BaseStorage<Product> {
    getMostExpensive(): Product {
        return this.items.reduce((acc, product) => (acc.price > product.price) ? acc : product, this.items[0]);
    }
}
```

---

**Пример использования**
```ts
const product1 = new Product("Phone", 500);
const product2 = new Product("Laptop", 1000);

const order1 = new Order(product1, 2);
const order2 = new Order(product2, 1);

const orderStorage = new OrderStorage();
orderStorage.addItem(order1);
orderStorage.addItem(order2);

console.log(orderStorage.getTotalValue()); // 2000
```
