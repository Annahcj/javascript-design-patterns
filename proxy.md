
# Proxy Design Pattern

The Proxy Pattern provides a surrogate or placeholder for another object.  

There are three types of proxy patterns:

1. Remote
2. Virtual
3. Protection

In this example, we will implement a virtual proxy.  
Virtual proxies cache information to postpone accessing the real object.  
Some information can take a long time to retrieve, so it is best to only call it when necessary.

The ToyotaCars class returns the price of the car when requested.  
The ToyotaCarsProxy fetches the price from the ToyotaCars class ONLY when it hasn't cached it yet.  
We call the getCarPrice method eight times, in the first four times, we call the actual ToyotaCars object, but in the remaining four times we are merely reading off our cache.   
Imagine that calls are much more frequent, and each time we call the ToyotaCars' getCarPrice method, it is much heavier and takes far longer.  

```
class ToyotaCars {
  getCarPrice(car) {
    if (car === 'Corolla') return '$50,400';
    else if (car === 'Camry') return '$52,800';
    else if (car === 'Prius') return '$48,100';
    else if (car === 'Yaris') return '$53,300';
  }
}

class ToyotaCarsProxy {
  constructor() {
    this.toyotaCars = new ToyotaCars();
    this.cache = {};
  }
  getCarPrice(car) {
    if (!this.cache[car]) {
      console.log('information fetched')
      this.cache[car] = this.toyotaCars.getCarPrice(car);
    } 
    return this.cache[car];
  }
}

const toyotaCarsProxy = new ToyotaCarsProxy();
console.log(toyotaCarsProxy.getCarPrice('Prius'))
console.log(toyotaCarsProxy.getCarPrice('Corolla'))
console.log(toyotaCarsProxy.getCarPrice('Camry'))
console.log(toyotaCarsProxy.getCarPrice('Yaris'))
console.log(toyotaCarsProxy.getCarPrice('Prius'))
console.log(toyotaCarsProxy.getCarPrice('Corolla'))
console.log(toyotaCarsProxy.getCarPrice('Camry'))
console.log(toyotaCarsProxy.getCarPrice('Yaris'))
```
