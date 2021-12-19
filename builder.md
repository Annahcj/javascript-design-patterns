# Builder Design Pattern

Create methods to change or add properties to an object.  

Without builder:  
```
class User {
  constructor(name, age, address) {
    this.name = name;
    this.age = age;
    this.address = address;
  }
}
let user = new User('Snoopy');
// age and address are undefined
user.age = 10;
user.address = '0 Unknown Street';
```

With builder:  
The code is tidier and we don't have to directly modify properties.  
The properties will also never be undefined.  

```
class User {
  constructor(name) {
    this.name = name;
  }
  setAge(age) {
    this.age = age;
    return this; // by returning this we can chain methods
  }
  setAddress(address) {
    this.address = address;
    return this;
  }
}
let user = new User('Snoopy').setAge(10).setAddress('0 Unknown Street');
```
