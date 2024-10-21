# Decorator Design Pattern

The decorator extends functionality of an object without changing the original object.  
It acts as a wrapper for the object.  

The main benefit is that it enables the client to dynamically extend and use any combination of functionality.
There can be multiple decorators, and each decorator follows the same interface as the original object.
The client can wrap the main object in multiple decorators and obtain all functionalities.

Implementation:
There are four main parts to the decorator pattern:
1. Base interface - interface of the base functionality
2. Concrete component - default functionality before extension, implements the base interface
3. Base decorator - all decorators extend from this class, takes in the wrappee and stores it as a field.
4. All other decorators - extends from the base decorator and each defines its own specific implementation.

``` 
interface Notifier {
  send(message: string): void;
}

// The default notification method and concrete class
class EmailNotifier implements Notifier {
  send(message: string) {
    console.log(`Sending ${message} via email`);
  }
}

// Base decorator
class NotifierDecorator implements EmailNotifier {
  private notifier: Notifier;

  constructor(notifier: Notifier) {
    this.notifier = notifier;
  }

  send(message: string) {
    this.notifier.send(message);
  }
}

class SmsNotifierDecorator extends NotifierDecorator {
  send(message: string) {
    console.log(`Sending ${message} via SMS`);
    super.send(message);
  }
}

class SlackNotifierDecorator extends NotifierDecorator {
  send(message: string) {
    console.log(`Sending ${message} via Slack`);
    super.send(message);
  }
}

// client
const notifier = new EmailNotifier();
const smsNotifier = new SmsNotifierDecorator(notifier);
const slackNotifierDecorator = new SlackNotifierDecorator(smsNotifier);

slackNotifierDecorator.send('This is an important message');
```
