# Abstract Factory Design Pattern

An abstract factory creates objects that are related by a common theme. 

In the code below, both the RaceCar and ToyCar share a common theme and have the same interface.  
This way, the client will be able to treat them in the same way.  
  
```
class RaceCar {
  constructor(name) {
    this.name = name;
  }
  getDetails() {
    console.log(`I am a ${this.name} racecar`);
  }
}

class ToyCar {
  constructor(name) {
    this.name = name;
  }
  getDetails() {
    console.log(`I am a ${this.name} toycar`);
  }
}

let ferrari = new RaceCar('ferrari');
let legoCar = new ToyCar('lego');

ferrari.getDetails();
legoCar.getDetails();
```