# Adapter Design Pattern

The adapter design pattern lets incompatible interfaces work together.    
It works like a real world adapter, adapting to the new interface so that it can work with the existing interface.   
It is also useful because we don't have to modify the existing source code and potentially cause bugs.  

In the example below, the payPal accepts payment in dollars, 
and the new payment method, googlePay, accepts payment in cents.  
The payment adapter converts the payment amount to cents, and makes the payment through googlePay.  

```
// old payment method
class Paypal {
  constructor(name) {
    this.name = name;
  }
  makePayment(amount) {
    console.log(`payment of ${amount} made through ${this.name} dollars`);
  }
}

// new payment method 
class GooglePay {
  constructor(name) {
    this.name = name;
  }
  pay(amount) {
    console.log(`payment of ${amount} cents made through ${this.name}`);
  }
}

// payment adapter: converts dollars to cents to fit the new payment method
class PaymentAdapter {
  constructor() {
    this.googlePay = new GooglePay('googlePay');
  }
  makePayment(amount) {
    amount = amount * 10;
    this.googlePay.pay(amount);
  }
}

let paymentAdapter = new PaymentAdapter();
paymentAdapter.makePayment(100); // payment of 1000 cents made through googlePay
```