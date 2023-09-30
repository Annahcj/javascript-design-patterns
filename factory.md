# Factory Design Pattern

A factory is an object which creates other objects.  
A factory Method defines a method, which should be used for creating objects instead of direct constructor call.  
It solves the problem of creating product objects without specifying their concrete classes.  

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
