# Memento Design Pattern

The memento design pattern enables an object to take a snapshot of its state.  
The mementos are stored in an object CareTaker, which keeps track of every memento and returns the requested memento.   

Participants:  
* Memento - the snapshot of state.  
* Originator - the original object.  
* CareTaker - manages the mementos.  

```
class Memento {
  constructor(state) {
    this.state = {
      name: state.name,
      age: state.age
    }
  }
  getState() {
    return this.state;
  }
}

class Originator {
  constructor(name, age) {
    this.state = { name, age };
  }
  setName(name) {
    this.state.name = name;
  }
  setAge(age) {
    this.state.age = age;
  }
  saveState() {
    return new Memento(this.state);
  }
  restoreState(memento) {
    this.state = memento.getState();
  }
}

class CareTaker {
  constructor() {
    this.mementos = [];
  }
  addMemento(memento) {
    this.mementos.push(memento);
  }
  getMemento(idx) {
    if (idx < 0 || idx >= this.mementos.length) return null;
    return this.mementos[idx];
  }
}

let caretaker = new CareTaker();
let person = new Originator('anna', 10);
caretaker.addMemento(person.saveState()); // memento is stored at index 0
person.setName('snoopy');
caretaker.addMemento(person.saveState()); // memento is stored at index 1
person.setAge(5);
person.restoreState(caretaker.getMemento(0)); // restores back to first state

console.log(person)
```
