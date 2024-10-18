# Decorator Design Pattern

The decorator extends functionality of an object without changing the original object.  
It acts as a wrapper for the object.  

The main benefit is that it enables the client to dynamically extend and use any combination of functionality.
There can be multiple decorators, and each decorator follows the same interface as the original object.
The client can wrap the main object in multiple decorators and obtain all functionalities.

Without this design pattern, sub-classes would need to be made to account for every combination of classes.

``` 
function User(name) {
  this.name = name;
  this.say = () => {
    console.log(`name: ${this.name}`)
  }
}

function DecoratedUser(user, city) {
  this.user = user;
  this.name = user.name;
  this.city = city;

  this.say = () => {
    console.log(`${this.name} lives in ${this.city}`)
  }
}

let user = new User('Bob');
user.say(); // Name: Bob

let decoratedUser = new DecoratedUser(user, 'Tokyo');
decoratedUser.say(); // Bob lives in Tokyo
```
