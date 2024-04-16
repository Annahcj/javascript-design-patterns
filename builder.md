# Builder Design Pattern

Separates the construction of complex objects from the orchestration so that the same construction process can create different representations

The structure of the builder pattern consists of two parts: The director and the builder.
The builder is an interface defining the "building blocks".
The director is responsible for orchestrating the creation of the final object, using methods defined by a builder class. It constructs the final object step-by-step.

What is promotes:
- Separates the building blocks (builder) with the building process (director).
- Step-by-step construction of complex objects.
- Encapsulation and modularization.

Use-cases:
- You need to create different representations of the same type of object.

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