# Chain of Responsibility Design Pattern

The chain of responsibility design patterns 'chains' objects into a linear sequence.  
Each object decides whether to deal with or pass it on to the next handler.  

Imagine we are implementing a program for validating a bank withdraw request.  
At first, we are only told to check the validity of the accountId and password, but over time, we are required to add more concrete validation.    
Our code could get quite messy and hard to manage, and this is where the chain of responsibility design pattern helps to simplify our code.    

Dynamically set the next handlers for each object with a method setNext.  
If any of the handlers has an error, it will not call the next handler.  
The chain of responsibility now makes it much easier for us to add new handlers and change the order of the chain.  

To illustrate the code below:  
### AccountValidator -> PasswordValidator -> BankWithdraw  

```
class AccountValidator {
  constructor() {
    this.accounts = new Set(['1021', '1022']);
  }
  setNext(handler) {
    this.next = handler;
    return handler;
  }
  handle(accountId, password, amount) {
    if (!this.accounts.has(accountId)) return false;
    return this.next.handle(accountId, password, amount);
  }
}

class PasswordValidator {
  constructor() {
    this.passwords = {
      '1021': 'afq211',
      '1022': 'gbo378'
    }
  }
  setNext(handler) {
    this.next = handler;
    return handler;
  }
  handle(accountId, password, amount) {
    if (this.passwords[accountId] !== password) return false;
    return this.next.handle(accountId, amount);
  }
}

class BankWithdraw {
  constructor() {
    this.bankDetails = {
      '1021': 100,
      '1022': 200
    }
  }
  handle(accountId, amount) {
    if (this.bankDetails[accountId] >= amount) {
      return true;
    }
    return false;
  }
}

const accountValidator = new AccountValidator();
const passwordValidator = new PasswordValidator();
const bankWithdraw = new BankWithdraw();

accountValidator.setNext(passwordValidator); // dynamically set next handlers
passwordValidator.setNext(bankWithdraw);

const canWithdraw = accountValidator.handle('1021', 'afq211', 50); // call the first in the chain
console.log(canWithdraw) // true
```