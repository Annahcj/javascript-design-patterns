# Template Design Pattern

The template design pattern gives a template or a skeleton.  
It lets subclasses redefine certain steps of an algorithm without changing the algorithm's structure.  
Subclasses get the algorithm's structure and have the option of redefining certain steps.   

Certain parts of the algorithm do not change, and some can be redefined.  

Why it is used:  
* To avoid code duplication when subclasses have common behavior.
* To give extensibility to subclasses.

```
class CarTemplate {
  constructor(name) {
    this.name = name;
  }
  getName() {
    console.log(`car name: ${this.name}`);
  }
  start() {
    console.log('Vroom vroom!');
  }
  stop() {
    console.log('Car has stopped');
  }
}

class RaceCar extends CarTemplate {
  start() {
    console.log('Roar! Vroom!');
  }
  stop() {
    console.log('Screech! Car has stopped');
  }
}

class ToyCar extends CarTemplate {
  start() {
    console.log('This car has no engine');
  }
  stop() {
    console.log('This car has no engine');
  }
}

let ferrari = new RaceCar('ferrari');
ferrari.start();
ferrari.getName();
let toycar = new ToyCar('toycar');
toycar.start();
toycar.getName();
```