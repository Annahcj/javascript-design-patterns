# Visitor Design Pattern

The visitor pattern adds new operations to existing object structures without modifying the structures.  

It is useful when:  
* Operations are not related to the object and you don't want to pollute the classes.  
* You don't want to change the existing structure but need to perform operations.

In the example below, the Car accepts the visitor and give it permission to 'visit' it. 
The CarPainterVisitor visits the car and paints the car.  

```
class Car {
  constructor(name, color) {
    this.name = name;
    this.color = color
  }
  setName(name) {
    this.name = name;
  }
  setColor(color) {
    this.color = color;
  }
  accept(visitor) {
    visitor.visit(this);
  }
}

class CarPainterVisitor {
  constructor(color) {
    this.color = color;
  }
  visit(car) {
    car.setColor(this.color);
  }
}

const car = new Car('tesla', 'white');
const carPainter = new CarPainterVisitor('blue');
car.accept(carPainter);
console.log(car) // car color is now blue
```