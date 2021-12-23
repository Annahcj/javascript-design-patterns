# Singleton Design Pattern

The singleton ensures an object only has one instance.  
getInstance: If the instance hasn't been created yet, create it. Return the instance.

```
class Singleton {
  createInstance() { // creates the instance
    return {name: 'The only instance'};
  }
  getInstance() { 
    if (!this.instance) {
      this.instance = this.createInstance();
    }
    return this.instance;
  }
}

const singleton = new Singleton();
const instance1 = singleton.getInstance();
const instance2 = singleton.getInstance();
console.log(instance1 === instance2) // true, they are both the same instance
```