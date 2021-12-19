# Iterator Design Pattern

An iterator provides a way to access each element sequentially without exposing the underlying representation.  
Basically, without having to check whether we have reached the end of the array of not, we can keep accessing the next element in the array.  
The iterator usually has the methods hasNext (returns whether we still have elements left to iterate over), and next (returns the next element)  

```
var Iterator = function(arr) {
  this.arr = arr;
  this.index = 0;
}

Iterator.prototype.hasNext = function() {
  return this.index < this.arr.length;
}

Iterator.prototype.next = function() {
  return this.arr[this.index++];
}

let iterator = new Iterator([1,2,3,4,5]);
console.log(iterator.hasNext()) // true
console.log(iterator.next()) // 1
console.log(iterator.next()) // 2
console.log(iterator.next()) // 3
console.log(iterator.next()) // 4
console.log(iterator.next()) // 5
console.log(iterator.hasNext()) // false
```
