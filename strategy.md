# Strategy Design Pattern

The strategy design pattern enables the use of various algorithms interchangably.  
Let's say we make a new class Car. The Car class has a method called start (starting the car).  
So, let's create a new Car, which inherits all the methods and properties.  

The problem occurs when a child needs a different method than the one given from the parent.  
So, we can use the strategy design pattern to ensure that the main code can remain untouched.  

We create a setStartBehavior function which takes in a startBehavior class and sets it to the startBehavior.  
The performStart function merely calls the start method of this.startBehavior, and whatever the startBehavior is, it outputs it accordingly.  
Essentially we are making the startBehavior dynamic and flexible according to the type of startBehavior the car uses.  

```
class Car {
  constructor(brand) {
    this.brand = brand;
    this.startBehavior;
  }
  setStartBehavior(startBehavior) {
    this.startBehavior = startBehavior;
  }
  performStart() {
    this.startBehavior.start();
  }
}

class CarStartBehavior {
  start() {
    console.log('Vroom vroom!')
  }
}

class NoStartBehavior {
  start() {
    console.log('Cannot start car. This car has no engine.')
  }
}

const car = new Car('toyota');
car.setStartBehavior(new CarStartBehavior()); // pass in the CarStartBehavior
car.performStart(); // 'Vroom vroom!'

const toyCar = new Car('toy car');
toyCar.setStartBehavior(new NoStartBehavior()); // pass in the NoStartBehavior
toyCar.performStart(); // 'Cannot start car. This car has no engine.'
```