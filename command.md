# Command Design Pattern

The command pattern supports undoable operations.
Create a class for each command.

Each command has an execute and undo method  
Stores the value to add (value to add, value to subtract, value to multiply, etc for this example) in the constructor  
For the execute and undo method, the current value is passed in, and we return the new value.  

The main class keeps a history of the commands.  
If we want to undo an operation, we pop it off the history and undo the command.  

```
class Calculator {
  constructor() {
    this.value = 0;
    this.commandHistory = [];
  }
  executeCommand(command) {
    this.value = command.execute(this.value);
    this.commandHistory.push(command);
  }
  undo() {
    let lastCommand = this.commandHistory.pop();
    this.value = lastCommand.undo(this.value);
  }
}

class AddCommand {
  constructor(valueToAdd) {
    this.valueToAdd = valueToAdd;
  }
  execute(currentValue) {
    return currentValue + this.valueToAdd;
  }
  undo(currentValue) {
    return currentValue - this.valueToAdd;
  }
}

class SubtractCommand {
  constructor(valueToSubtract) {
    this.valueToSubtract = valueToSubtract;
  }
  execute(currentValue) {
    return currentValue - this.valueToSubtract;
  }
  undo(currentValue) {
    return currentValue + this.valueToSubtract;
  }
}

class MultiplyCommand {
  constructor(valueToMultiply) {
    this.valueToMultiply = valueToMultiply;
  }
  execute(currentValue) {
    return currentValue * this.valueToMultiply;
  }
  undo(currentValue) {
    return currentValue / this.valueToMultiply;
  }
}

class AddAndMultiplyCommand { // we can also combine commands into one command
  constructor(valueToAdd, valueToMultiply) {
    this.addCommand = new AddCommand(valueToAdd);
    this.multiplyCommand = new MultiplyCommand(valueToMultiply);
  }
  execute(currentValue) {
    let newValue = this.addCommand.execute(currentValue);
    return this.multiplyCommand.execute(newValue);
  }
  undo(currentValue) {
    let newValue = this.multiplyCommand.undo(currentValue);
    return this.addCommand.undo(newValue);
  }
}

const calc = new Calculator();
calc.executeCommand(new AddCommand(10)); // value: 10
calc.undo(); // value: 0
calc.executeCommand(new AddCommand(5)); // value: 5
calc.executeCommand(new SubtractCommand(5)) // value: 0
calc.undo(); // value: 5
calc.executeCommand(new AddAndMultiplyCommand(5, 2)); // value: 20
calc.undo(); // value: 5
console.log(calc)
```