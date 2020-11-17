<h1 align="center">
Freezing-Objects
</h1>

A reducer must never mutate its arguements.

If the state changes, the reducer must return a new object.

JS provides us with an easy way to enforce this using Object.freeze.

Object.freeze prevents new props from being added to an object.

Object.freeze also prevents props currently on an object from being altered.
