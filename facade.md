# Facade Design Pattern

The facade design pattern provides a simpler interface for the client.  
The facade accesses subsystems with complex logic, and creates a system that is easier to use.  

```
class Circle {
  draw() { // let's imagine that there is complex code 
    console.log('A circle has been drawn.')
  }
}

class Square {
  draw() { 
    console.log('A square has been drawn.')
  }
}

class Rectangle {
  draw() {
    console.log('A rectangle has been drawn.')
  }
}

class ShapeDrawer {
  drawCircle() {
    new Circle().draw(); // accesses subsystems
  }
  drawSquare() {
    new Square().draw();
  }
  drawRectangle() {
    new Rectangle().draw();
  }
}

let shapeDrawer = new ShapeDrawer();
shapeDrawer.drawCircle(); // simple interface
shapeDrawer.drawSquare();
shapeDrawer.drawRectangle();
```