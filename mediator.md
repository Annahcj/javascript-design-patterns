# Mediator Design Pattern

The mediator acts as a control tower for other objects.  
The other objects have no information about and do not deal with the other objects apart from the mediator.  
The mediator is an abstraction layer that simplifies the way objects interact with each other.  

In this example, although users send messages to other users, they do so by going through the mediator.  
The mediator handles all the controlling and directing.  

This is useful when interaction between objects are complex and hard to manage.  

```
class Mediator {
  sendMessage(message, sender, receiver) {
    receiver.receiveMessage(message, sender);
  }
}

class User {
  constructor(name, mediator) {
    this.name = name;
    this.mediator = mediator;
  }
  sendMessage(message, receiver) {
    this.mediator.sendMessage(message, this, receiver);
  }
  receiveMessage(message, sender) {
    console.log(`${sender.name} -> ${this.name}: ${message}`)
  }
}

const chatroom = new Mediator();
const alice = new User('alice', chatroom);
const bob = new User('bob', chatroom);
const mary = new User('mary', chatroom);

alice.sendMessage('Hello Bob', bob);
bob.sendMessage('Hello Alice', alice);
alice.sendMessage('Mary, are you free?', mary);
mary.sendMessage('Yes', alice);
alice.sendMessage('Cool, let\'s go have lunch', mary);
mary.sendMessage('Sounds good! I know a good restaurant...', alice);

// output:
// alice -> bob: Hello Bob
// bob -> alice: Hello Alice
// alice -> mary: Mary, are you free?
// mary -> alice: Yes
// alice -> mary: Cool, let's go have lunch
// mary -> alice: Sounds good! I know a good restaurant...
```