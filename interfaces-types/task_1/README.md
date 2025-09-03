# Задача

Есть класс `Api`, предназначенный для работы с заметками и списком дел. Есть также две функции: одна отображает заметки,
а другая — список дел.

Функции принимают аргументом экземпляр класса `Api`. Однако им не нужно знать про все методы `Api`. Для функции
`renderPosts` достаточно методов для работы с заметками, а `renderTodos` ограничится напоминаниями.

Разделите методы класса `Api` на две части. Опишите их двумя интерфейсами:

* Интерфейс `PostsApi` должен описывать методы для работы с заметками.
* Интерфейс `TodosApi` должен описывать взаимодействие со списком дел.

Сделайте так, чтобы класс `Api` реализовывал эти два интерфейса.

```ts
interface Post {
    id: string;
    title: string;
}

interface Todo {
    id: string;
    todo: string;
    isReady?: boolean;
}

// Опишите интерфейс PostsApi


// Опишите интерфейс TodosApi


// Имплементируйте в классе интерфейсы PostsApi и TodosApi
class Api {
    private idCounter: number;

    protected posts: Post[];
    protected todos: Todo[];

    constructor() {
        this.idCounter = 0;
        this.posts = [];
        this.todos = [];
    }

    protected makeId() {
        return String(this.idCounter++);
    }

    getPosts(limit: number = 5, offset: number = 0) {
        return this.posts.slice(offset, limit);
    }

    makePost(title: string) {
        const post = {
            id: this.makeId(),
            title,
        }

        this.posts.push(post);

        return post;
    }

    updatePost(id: string, data: Post) {
        const post = this.posts.find(post => post.id === id);

        if (post) {
            Object.assign(post, data);
        }
    }

    deletePost(id: string): void {
        this.posts = this.posts.filter(post => post.id !== id);
    }

    getTodos(): Todo[] {
        return this.todos;
    }

    newTodo(todo: string): Todo {
        const todoItem = {
            id: this.makeId(),
            todo,
        }

        this.todos.push(todoItem);

        return todoItem;
    }

    readyTodo(id: string): void {
        const todo = this.todos.find(todo => todo.id === id);

        if (todo) {
            todo.isReady = true
        }
    }
}

function renderPosts(api: PostsApi) {
    const posts = api.getPosts();

    return posts.map((post, index) => `${index + 1}. ${post.title}`);
}

function renderTodos(api: TodosApi) {
    const todos = api.getTodos();

    todos.sort((first, second) => {
        if (!first.isReady && second.isReady) {
            return -1;
        }

        return 1;
    });

    return todos.map(item => `[${item.isReady ? 1 : 0}] ${item.todo}`);
}

const myApi = new Api();

myApi.makePost('Как сесть на шпагат русалке');
myApi.makePost('Дружба с бэкендером: за и против');
myApi.makePost('Три богатыря (не меньше)');

console.log(renderPosts(myApi));

myApi.newTodo('Погладить носки');
myApi.newTodo('Покрасить траву');
const { id } = myApi.newTodo('Вдохнуть воздуха');

myApi.readyTodo(id);

console.log(renderTodos(myApi));
```