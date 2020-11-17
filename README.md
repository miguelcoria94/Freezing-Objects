<h1 align="center">
Freezing-Objects
</h1>

A reducer must never mutate its arguements.

If the state changes, the reducer must return a new object.

JS provides us with an easy way to enforce this using Object.freeze.

Object.freeze prevents new props from being added to an object.

Object.freeze also prevents props currently on an object from being altered.

<h1 align="center">
Using Object.freeze to prevent state mutations
</h1>

By calling Object.freeze(state) at the top of every reducer, you can ensure that the state is never accidentally mutated. For example, this is what your farmer reducer from the Fruit Stand application would look like:

```js
    const farmersReducer = (state = {}, action) => {
        Object.freeze(state);
        let nextState = Object.assign({}, state);
        switch (action.type) {
            case HIRE_FARMER:
            const farmerToHire = {
                id: action.id,
                name: action.name,
                paid: false
            };
            nextState[action.id] = farmerToHire;
            return nextState;
            case PAY_FARMER:
            const farmerToPay = nextState[action.id];
            farmerToPay.paid = !farmerToPay.paid;
            return nextState;
            default:
            return state;
        }
    };
```

Now you can be certain that you won't accidentally mutate the state within the reducer.

<h1 align="center">
Understanding the difference between deep and shallow freezes
</h1>

example:

```js
const people = { farmers: { name: 'Old MacDonald' } };
Object.freeze(people);
```

When you try to mutate an object that you froze by modifying a property, it will be prevented:

```js
people.farmers = { name: 'Young MacDonald' };
people; // { farmers: { name: 'Old MacDonald' } }
```

Note: This is not a deep freeze. Object.freeze performs a shallow freeze as it only applies to the immediate properties of the object itself. Nested objects can still be mutated, so be careful. Here's an example of this:

```js
people.farmers.name = 'Young MacDonald';
people; // { farmers: { name: 'Young MacDonald' } }
```


<h1 align="center">
Object.freeze and arrays
</h1>

You can also use Object.freeze to freeze an array, so if a reducer's state parameter is an array, you can still prevent accidental state mutations: