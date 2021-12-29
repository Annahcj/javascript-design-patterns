# State Design Pattern

State is a behavioral design pattern that lets an object alter its behavior when its internal state changes.  
Each state of an object has its own class, and each state class must follow the same interface.  

It shares similarities with the Strategy Pattern, however the difference is that the state in the State Pattern knows and accesses other states, 
whereas strategies don't know each other.

In the example below, we are simulating a game.  
The game has three states: ReadyState, PlayingState, and StopState.  
The game is initialized with the ReadyState, and is switched out when certain state changes.  

For example, when play() is called within the ReadyState, Game switches the state to PlayingState.  
When pause() is called within PlayingState, Game switches out the state to StopState.  

```
class Game {
  constructor() {
    this.state = new ReadyState(this);
  }
  changeState(state) {
    this.state = state;
  }
  play() {
    this.state.play();
  }
  pause() {
    this.state.pause();
  }
}

class ReadyState {
  constructor(game) {
    this.game = game;
  }
  play() {
    console.log('Switched from ReadyState to PlayingState');
    this.game.changeState(new PlayingState(this.game));
  }
  pause() {
    console.log('Switched from ReadyState to StopState');
    this.game.changeState(new PlayingState(this.game));
  }
}

class PlayingState {
  constructor(game) {
    this.game = game;
  }
  play() {
    console.log('already playing');
  }
  pause() {
    console.log('Switched from PlayingState to StopState');
    this.game.changeState(new StopState(this.game));
  }
}

class StopState {
  constructor(game) {
    this.game = game;
  }
  play() {
    console.log('Switched from StopState to PlayingState');
    this.game.changeState(new PlayingState(this.game));
  }
  pause() {
    console.log('already paused');
  }
}

let game = new Game();
game.play(); // Switched from ReadyState to PlayingState
game.pause(); // Switched from PlayingState to StopState
game.play(); // Switched from StopState to PlayingState
game.pause(); // Switched from PlayingState to StopState
```