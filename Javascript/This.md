<h1>This</h1>

Some ways to get understand the `this`in javascript.

```javascript
console.log(this);
```
Doing this in a page you get window object
```javascript
Window {postMessage: ƒ, blur: ƒ, focus: ƒ, close: ƒ, frames: Window, …}
```

```javascript
function calculateAge(bornYear){
  console.log(2018-bornYear);
  console.log(this);
}

calculateAge(1995);
```

The `this` here still represents the window object because this is a regular function call, not a method.

```javascript
var dog = {
    name : 'Farrusco',
    yearofBirth : 2016,
    calculateAge : function(){
        console.log(this);
        console.log(2018 -this.yearofBirth)

        function innerFunction(){
            console.log(this);
        }
        innerFunction();
    }
}

dog.calculateAge()
```
So here the `this`(inside the `calculateAge` function) is the dog object.But the this inside the innerFunction represents the window, because it´s not a method, even that is a function inside the function that represents the method...Yeap.





