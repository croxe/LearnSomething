# Ch 3 Fundamental Data structure

### Ch 3.1 Using Arrays

```java
public class GameEntry {
  private String name; // name of the person earning this score
  private int score; // the score value
  /∗∗ Constructs a game entry with given parameters.. ∗/
  public GameEntry(String n, int s) {
  name = n;
  score = s;
  }
  /∗∗ Returns the name field. ∗/
  public String getName() { return name; }
  /∗∗ Returns the score field. ∗/
  public int getScore() { return score; }
  /∗∗ Returns a string representation of this entry. ∗/
  public String toString() {
  return "(" + name + ", " + score + ")";
  }
}
```

```java
/∗∗ Class for storing high scores in an array in nondecreasing order. ∗/
public class Scoreboard {
  private int numEntries = 0; // number of actual entries
  private GameEntry[ ] board; // array of game entries (names & scores)
  /∗∗ Constructs an empty scoreboard with the given capacity for storing entries. ∗/6 public Scoreboard(int capacity) {
  board = new GameEntry[capacity];
  }
... // more methods will go here
}
```

```java
/∗∗ Attempt to add a new score to the collection (if it is high enough) ∗/
public void add(GameEntry e) {
  int newScore = e.getScore();
  // is the new entry e really a high score?
  if (numEntries < board.length || newScore > board[numEntries−1].getScore()) {
    if (numEntries < board.length) // no score drops from the board
      numEntries++; // so overall number increases
      // shift any lower scores rightward to make room for the new entry
      int j = numEntries − 1;
      while (j > 0 && board[j−1].getScore() < newScore) {
      board[j] = board[j−1]; // shift entry from j-1 to j
      j−−; // and decrement j
    }
    board[j] = e; // when done, add new entry
  }
}
```