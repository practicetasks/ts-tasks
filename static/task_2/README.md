
# Задача

1. Реализуйте все методы так, чтобы статистика обновлялась корректно
2. При создании новой сессии должен увеличиваться счетчик игр
3. Метод `addPoints()` должен обновлять рекорд, если текущий счет больше
4. `endGame()` должен сохранить финальный результат в общий массив
5. `getAverageScore()` должен правильно считать среднее
6. `getTopScores()` должен возвращать 3 лучших результата по убыванию

```typescript
class GameSession {
  private playerName: string;
  private currentScore: number = 0;
  
  // Статические поля для общей статистики
  private static totalGamesPlayed: number = 0;
  private static highScore: number = 0;
  private static bestPlayer: string = "";
  private static allScores: number[] = [];
  
  constructor(playerName: string) {
    this.playerName = playerName;
    // Что нужно сделать при создании новой сессии?
  }
  
  public addPoints(points: number): void {
    this.currentScore += points;
    // Нужно ли обновить статические поля?
  }
  
  public endGame(): void {
    // Что происходит когда игра заканчивается?
    // Как сохранить результат в общую статистику?
  }
  
  // Статические методы для получения статистики
  public static getHighScore(): number {
    // Вернуть рекордный счет
  }
  
  public static getBestPlayer(): string {
    // Вернуть имя лучшего игрока
  }
  
  public static getAverageScore(): number {
    // Вычислить средний счет по всем играм
  }
  
  public static getTotalGames(): number {
    // Вернуть общее количество сыгранных игр
  }
  
  public static resetStats(): void {
    // Сбросить всю статистику
  }
  
  // Бонус: статический метод для получения топ-3 результатов
  public static getTopScores(): number[] {
    // Вернуть массив из 3 лучших результатов
  }
  
  public getCurrentScore(): number {
    return this.currentScore;
  }
  
  public getPlayerName(): string {
    return this.playerName;
  }
}
```

**Пример использования:**
```typescript
const game1 = new GameSession("Alice");
game1.addPoints(100);
game1.addPoints(50);
game1.endGame();

const game2 = new GameSession("Bob");
game2.addPoints(200);
game2.endGame();

console.log(GameSession.getHighScore()); // 200
console.log(GameSession.getBestPlayer()); // "Bob"
console.log(GameSession.getTotalGames()); // 2
```

