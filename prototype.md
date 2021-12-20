# Prototype Design Pattern

The prototype pattern supports cloning based on a template.  
We can clone the prototype into a new object initialized with the values of the prototype.  
Simply speaking, we can make a copy of an object with existing values already.  

This is useful when we want to have a set template which we will use many times.  

```
function UserPrototype(prototype) {
  this.prototype = prototype;
  this.clone = () => {
    let clone = new User();
    clone.name = this.prototype.name;
    clone.email = this.prototype.name;
    return clone;
  }
}

function User(name, email) {
  this.name = name;
  this.email = email;
  this.printName = () => {
    console.log(`name: ${this.name}`)
  }
}

let user = new User('Snoopy', 'snoopy@gmail.com'); 
let userPrototype = new UserPrototype(user); 
let userClone = userPrototype.clone();
userClone.printName(); // name: Snoopy
```