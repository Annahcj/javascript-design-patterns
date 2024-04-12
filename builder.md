# Builder Design Pattern

Separates the construction of complex objects from the orchestration so that the same construction process can create different representations.

The structure of the builder pattern consists of two parts: The director and the builder.
The builder is an interface defining common methods to be implemented when extended.
The director is responsible for creating the final object, using methods defined by a builder class.

Why you would use it:
- Ensures that the director doesn't need to change when we create a new type of builder, since the new builder implements the same interface.
- Separates the construction of the builder object with how they are assembled at the end.
- Promotes the open-closed principle (open for extension, closed for modification)


Example:
```
// Builder interface
interface PizzaBuilder {
  name: string;
  base: string;
  toppings: string[];
  setName: () => this;
  setBase: () => this;
  setToppings: () => this;
}

class HawaiianPizzaBuilder implements PizzaBuilder {
  name: string;
  base: string;
  toppings: string[];

  public setName() {
    this.name = 'Hawaiian';
    return this;
  }

  public setBase() {
    this.base = 'Dough';
    return this;
  }

  public setToppings() {
    this.toppings = ['Pineapple', 'Ham', 'Cheese'];
    return this;
  }
}

class PepperoniPizzaBuilder implements PizzaBuilder {
  name: string;
  base: string;
  toppings: string[];

  public setName() {
    this.name = 'Pepperoni';
    return this;
  }

  public setBase() {
    this.base = 'Dough';
    return this;
  }

  public setToppings() {
    this.toppings = ['Pepperoni', 'Cheese'];
    return this;
  }
}

// Director
class PizzaMaker {
  pizzaBuilder: PizzaBuilder;

  constructor(pizzaBuilder: PizzaBuilder) {
    this.pizzaBuilder = pizzaBuilder;
  }
  makePizza() {
    return this.pizzaBuilder.setName().setBase().setToppings();
  }
}

const myPizza = new PizzaMaker(new HawaiianPizzaBuilder()).makePizza();
```

Example without director:
```
interface PizzaBuilder {
  name: string;
  base: string;
  toppings: string[];
  setName: () => this;
  setBase: () => this;
  setToppings: () => this;
}

class HawaiianPizzaBuilder implements PizzaBuilder {
  name: string;
  base: string;
  toppings: string[];

  public setName() {
    this.name = 'Hawaiian';
    return this;
  }

  public setBase() {
    this.base = 'Dough';
    return this;
  }

  public setToppings() {
    this.toppings = ['Pineapple', 'Ham', 'Cheese'];
    return this;
  }
}

class PepperoniPizzaBuilder implements PizzaBuilder {
  name: string;
  base: string;
  toppings: string[];

  public setName() {
    this.name = 'Pepperoni';
    return this;
  }

  public setBase() {
    this.base = 'Dough';
    return this;
  }

  public setToppings() {
    this.toppings = ['Pepperoni', 'Cheese'];
    return this;
  }
}

const myPizza = new HawaiianPizzaBuilder().setName().setBase().setToppings();
```