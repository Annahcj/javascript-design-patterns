# Flyweight Design Pattern

The flyweight design pattern uses sharing to support a large quantity of fine-grained objects efficiently.  

Imagine we are creating a game which renders hundreds of thousands of trees.  
There are only a few type of trees, but each tree is an object which contains a large amount of information.    
Since many of the trees are of the same type, we can use a flyweight pattern to share the information for each tree type.  

Flyweight Factory:
A flyweight factory caches flyweights containing the same state/information.  
getFlyweight method: if the cache doesn't contain a flyweight with the given state, creates a new flyweight and saves in cache. 
otherwise, returns the flyweight that is stored in the cache.

```
class TreeFlyweight {
  constructor(name, color) {
    this.name = name;
    this.color = color;
  }
  draw(x, y) {
    console.log(`${this.name} tree drawn at location ${x} ${y}`);
  }
}

class TreeFlyweightFactory {
  constructor() {
    this.cache = {};
  }
  getTree(name, color) {
    if (!this.cache[`${name},${color}`]) {
      this.cache[`${name},${color}`] = new TreeFlyweight(name, color);
    }
    return this.cache[`${name},${color}`];
  }
}

class Tree {
  constructor(name, color) {
    this.flyweight = treeFlyweightFactory.getTree(name, color);
  }
  draw(x, y) {
    this.flyweight.draw(x, y);
  }
}

class Trees {
  constructor() {
    this.trees = [];
  }
  addTree(name, color) {
    let newTree = new Tree(name, color);
    this.trees.push(newTree);
  }
}

let treeFlyweightFactory = new TreeFlyweightFactory();
let forest = new Trees();
forest.addTree('oak', 'green');
forest.addTree('oak', 'green');
forest.addTree('oak', 'green');
forest.addTree('oak', 'green');
// cache: { 'oak,green': { name: 'oak', color: 'green' } }
// the same flyweight is shared among 4 different trees. 
```