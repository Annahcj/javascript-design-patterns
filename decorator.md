# Decorator Design Pattern

The decorator extends functionality of an object without changing the original object.  
It acts as a wrapper for the object.  

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
