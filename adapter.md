# Adapter Design Pattern

The adapter design pattern lets incompatible interfaces work together.    
This is often used when we need to avoid modifying the existing code.
It works like a real world adapter, converting the input to the expected format of the new interface.
In the client's perspective, nothing should change. The adapter abstracts all the conversion. 

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