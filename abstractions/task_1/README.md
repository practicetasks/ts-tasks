# Задача

В коде ниже класс `Block` описывает блочный элемент в HTML, а класс `Picture` — изображение. Но есть проблемы:

* Некоторые свойства и методы объектов повторяются, их реализация выполнена несколько раз. А любые повторения — это
  плохо.
* У класса `Block` могут быть внутренние элементы-потомки: строки, иные представители класса `Block`, изображения или
  другие элементы, о которых мы пока не знаем. И как эти внутренние элементы типизировать?!

Решить эти проблемы поможет абстрактный класс `View` — реализуйте его.

* Посмотрите внимательно, какие поля и методы повторяются, и унесите их в абстрактный класс. Затем сделайте так, чтобы
  классы `Block` и `Picture` его наследовали. Так вы избавитесь от дублирования логики.
* Некоторые поля и методы имеют разную реализацию, но суть у них одинаковая. Такие поля и методы можно также унести в
  абстрактный класс и сделать абстрактными.
* Поле `children` теперь будет содержать другие объекты класса View или строки. Не нужно знать, какие именно элементы
  будут потомками, главное, чтобы они наследовали класс `View`.

```ts
// TODO: Реализуйте абстрактный класс View


// TODO: Наследуйте класс View
class Block {
  tag = 'div';
  children: (View | string)[];
  id?: string;

  constructor(children?: (View | string)[], id?: string) {
    this.children = children || [];
    this.id = id;
  }

  renderChildren() {
    return this.children.map(child => {
      if (typeof child === 'string') {
        return child;
      }

      return child.render();
    }).join('');
  }

  renderHTML(attributes?: Record<string, string>) {
    const attributesString = Object.entries(attributes || {})
            .map(([key, value]) => ` ${key}="${value}"`).join('');

    const tag = this.tag;
    const childrenString = this.renderChildren();

    if (childrenString) {
      return `<${tag}${attributesString}>${childrenString}</${tag}>`;
    }

    return `<${tag}${attributesString} />`;
  }

  render() {
    return this.renderHTML(this.id ? { id: this.id } : undefined);
  }
}

// TODO: Наследуйте класс View
class Picture {
  tag = 'img';
  children: (View | string)[];
  src: string;
  title: string;

  constructor(src: string, title: string) {
    this.children = [];
    this.src = src;
    this.title = title;
  }

  renderChildren() {
    return this.children.map(child => {
      if (typeof child === 'string') {
        return child;
      }

      return child.render();
    }).join('');
  }

  renderHTML(attributes?: Record<string, string>) {
    const attributesString = Object.entries(attributes || {})
            .map(([key, value]) => ` ${key}="${value}"`).join('');

    const tag = this.tag;
    const childrenString = this.renderChildren();

    if (childrenString) {
      return `<${tag}${attributesString}>${childrenString}</${tag}>`;
    }

    return `<${tag}${attributesString} />`;
  }

  render() {
    return this.renderHTML({ src: this.src, alt: this.title });
  }
}

const image = new Picture('https://some.org/logo', 'Какой-то логотип');
const header = new Block([image, 'ООО "Космические аппараты"'], 'Header');

console.log(header.render());
```