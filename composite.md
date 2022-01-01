# Composite Design Pattern

A composite treats a composite object and an individual object in the same way.  
Composes objects into tree structures with  
* Individual objects as leaves (no children)  
* Composite objects as composites (objects which can have children)  

In the code below, both the Employee and the EmployeeComposite class can show the employee details in the same way.   
It makes no difference whether it is an Employee or an EmployeeComposite. It is treated in the same way.  

```
class Employee {
  constructor(name) {
    this.name = name;
  }
  showDetails() {
    console.log(`name: ${this.name}`)
  }
}

class EmployeeComposite {
  constructor() {
    this.items = [];
  }
  add(employee) {
    this.items.push(employee);
  }
  remove(employeeToRemove) {
    this.items = this.items.filter(employee => employee !== employeeToRemove);
  }
  showDetails() {
    for (var employee of this.items) {
      console.log(`name: ${employee.name}`)
    }
  }
}

const snoopy = new Employee('snoopy');
snoopy.showDetails(); // name: snoopy

const woodstock = new Employee('woodstock');
woodstock.showDetails(); // name: woodstock

const employees = new EmployeeComposite();
employees.add(snoopy);
employees.add(woodstock);

employees.showDetails(); // name: snoopy  name: woodstock
```
