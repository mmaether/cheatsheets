# JavaScript Cheat Sheet

Type | Description
---- | -----------
`var` | Creates a function-scoped or globally-scoped variable. 
`let` | Creates block-scoped local variables. Use this instead of `var`.
`const` | A variable that is a constant value.

## Arrow Functions

A typical JavaScript function may look like: 

```js
function myfunction() {

}
```

While an arror function looks like:

```js
const myFunction = () => {

}
```

Arrow functions help with the `this` keyword. 

It can be shortened further, as demonstrated below.

```js
const multiply = number => number * 2;
```