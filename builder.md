# Builder Design Pattern

Separates complex object construction into steps and gives flexibility to only call the methods necessary for the given use-case.
It also enables the construction of different representations of objects using the same construction process.

The structure of the builder pattern consists of two parts: The builder and the director.
The builder is the one that defines the object, and contain the different steps.
The director is responsible for orchestrating the creation of the final object, using methods defined by a builder class. It constructs the final object step-by-step.

What it promotes:
- Separates the building blocks (builder) with the building process (director).
- Step-by-step construction of complex objects, hence solving the problem of having unnecessary steps.
- Encapsulation and modularization.

Use-cases:
- You need to create different representations of the same type of object.
- You have unnecessary steps that don't get used most of the time.

Example:
```
// Builder
class PizzaBuilder {
  base: string;
  toppings: string[];

  public setBase() {
    this.base = 'Dough';
    return this;
  }

  public addHam() {
    this.toppings.push('Ham');
    return this;
  }

  public addCheese() {
    this.toppings.push('Cheese');
    return this;
  }

  public addPineapple() {
    this.toppings.push('Pineapple');
    return this;
  }

  public addPepperoni() {
    this.toppings.push('Pepperoni');
    return this;
  }
}

// Directors
class HawaiianPizzaMaker {
  pizzaBuilder: PizzaBuilder;

  constructor(pizzaBuilder: PizzaBuilder) {
    this.pizzaBuilder = pizzaBuilder;
  }
  makePizza() {
    return this.pizzaBuilder.setBase().addHam().addCheese().addPineapple();
  }
}

class PepperoniPizzaMaker {
  pizzaBuilder: PizzaBuilder;

  constructor(pizzaBuilder: PizzaBuilder) {
    this.pizzaBuilder = pizzaBuilder;
  }
  makePizza() {
    return this.pizzaBuilder.setBase().addCheese().addPepperoni();
  }
}

const myPizza = new PepperoniPizzaMaker(new PizzaBuilder()).makePizza();
```