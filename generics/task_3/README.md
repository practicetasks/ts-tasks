## Задача


### Условие

Опишите обобщённый интерфейс коллекции `Collection<T>` и реализуйте **два разных класса**, которые его имплементируют: `Stack<T>` (LIFO — последний пришёл, первый вышел) и `Queue<T>` (FIFO — первый пришёл, первый вышел).

```typescript
// Общий контракт для любой коллекции
interface Collection<T> {
  add(item: T): void;        // положить элемент
  remove(): T | undefined;   // достать элемент (по правилу коллекции)
  peek(): T | undefined;     // посмотреть следующий, не доставая
  get size(): number;        // количество элементов
  isEmpty(): boolean;        // пустая ли
}

class Stack<T> implements Collection<T> {
  // твоя реализация (LIFO)
}

class Queue<T> implements Collection<T> {
  // твоя реализация (FIFO)
}
```

### Требования

1. Интерфейс `Collection<T>` обобщённый — работает с элементами любого типа.
2. `Stack<T>` и `Queue<T>` **оба** реализуют `Collection<T>`, но `remove()` ведёт себя по-разному:
    - `Stack` достаёт **последний** добавленный элемент.
    - `Queue` достаёт **первый** добавленный элемент.
3. `peek()` показывает тот элемент, который вернёт следующий `remove()`, но не удаляет его.
4. `size` — геттер (`get size()`), а не метод.
5. Бонус-требование на полиморфизм: напишите функцию `drain<T>(collection: Collection<T>): T[]`, которая опустошает **любую** коллекцию (и стек, и очередь) и возвращает элементы в порядке извлечения. Функция должна работать через интерфейс, не зная конкретного класса.
6. Строгая типизация, без `any`.

### Пример использования

```typescript
const stack = new Stack<number>();
stack.add(1);
stack.add(2);
stack.add(3);

stack.peek();    // 3 (вершина стека)
stack.remove();  // 3
stack.remove();  // 2
stack.size;      // 1

const queue = new Queue<string>();
queue.add("Аня");
queue.add("Боря");
queue.add("Вера");

queue.peek();    // "Аня" (начало очереди)
queue.remove();  // "Аня"
queue.remove();  // "Боря"

// Полиморфизм: одна функция для обеих коллекций
const s = new Stack<number>();
s.add(1); s.add(2); s.add(3);
drain(s);   // [3, 2, 1]  — LIFO

const q = new Queue<number>();
q.add(1); q.add(2); q.add(3);
drain(q);   // [1, 2, 3]  — FIFO

// drain принимает Collection<T> — ему всё равно, стек это или очередь
```

