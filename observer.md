# Observer Design Pattern

The observer pattern consists of a Subject and Observers.  
When the Subject is changed, all the Observers are notified.  

Events and event handlers use the observer pattern.  

In this example we merely console.log the fact that an element has been notified, but in real cases, state may be passed so that the observers can be updated.  

```
class Subject {
  constructor() {
    this.observers = [];
  }
  addSubscriber(observer) {
    this.observers.push(observer);
  }
  removeSubscriber(observer) {
    this.observers = this.observers.filter(o => o !== observer);
  }
  notifyObservers() {
    for (var observer of this.observers) {
      observer.notify();
    }
  }
}

class Observer {
  constructor(name) {
    this.name = name;
  }
  notify() {
    console.log(`${this.name} has been notified`)
  }
}

const subject = new Subject();
const observer1 = new Observer('observer1');
const observer2 = new Observer('observer2');
subject.addSubscriber(observer1);
subject.addSubscriber(observer2);
subject.notifyObservers(); // observer1 has been notified, observer2 has been notified 

subject.removeSubscriber(observer2); 
subject.notifyObservers(); // observer1 has been notified
```
