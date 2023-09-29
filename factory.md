# Factory Design Pattern

A factory is an object which creates other objects.  
A factory Method defines a method, which should be used for creating objects instead of direct constructor call.  
It solves the problem of creating product objects without specifying their concrete classes.  

Advantages:
* Ensures that objects are created in a consistent manner, and defines a set of rules that becomes a common interface for each object created.
* e.g: You can create a common function that makes DB calls, and define a set of rules to ensure DB creation becomes safe for all types of DB operations.

```
function UserFactory() {
  this.create = type => {
    switch (type) {
    case 'student':
      return new StudentUser();
    case 'teacher':
      return new TeacherUser();
    default:
      return null;
    }
  }
}

function StudentUser() {
  this.hasAccess = false;
  this.say = () => {
    console.log("I am a student")
  }
}

function TeacherUser() {
  this.hasAccess = true;
  this.say = () => {
    console.log("I am a teacher")
  }
}

let userFactory = new UserFactory();
const student = userFactory.create('student');
student.say(); // I am a student
const teacher = userFactory.create('teacher');
teacher.say(); // I am a teacher
```
