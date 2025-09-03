# Вопрос

Перед вами пример класса, который описывает футбольную команду. Какие поля и методы можно сделать статическими?

```ts
interface Player {
    name: string;
    height: number;
}

class Team {
    // Необходимое количеcтво игроков на поле, константа
    playersOnTheField = 11;

    // Хранит все существующие команды
    allTeams: Team[] = [];

    // Название команды
    name: string;

    // Игроки команды
    players: Player[];

    // Количество кубков, которые выиграла команда 
    cups: number;

    constructor(name: string, cups?: number) {
        this.name = name;
        this.players = [];
        this.cups = cups || 0;

        this.allTeams.push(this);
    }

    // Сравнивает две команды по количеству кубков
    compare(t1: Team, t2: Team) {
        return t2.cups - t1.cups;
    }

    // Отмечает победу команды на кубке
    win() {
        this.cups++;
    }

    // Клонирует команду (в параллельной Вселенной)
    clone(team: Team) {
        const clone = new Team(team.name, team.cups);

        team.players.forEach(clone.addPlayer);

        return clone;
    }

    // Возвращает количество существующих команд
    get totalTeamsCount() {
        return this.allTeams.length;
    }

    // Добавляет нового игрока в команду
    addPlayer(guy: Player) {
        this.players.push(guy);
    }
}
```