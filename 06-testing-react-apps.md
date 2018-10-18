# Testing React Components (work-in-progress)
An important benefit of decoupling from the actual DOM implementation and working at a higher level of abstraction in JavaScript is that we can easily test React components. If you think about it, a component is not radically different than an object or a function, gets some inputs, performs some actions and returns a value (JSX in this case). 

## Jest
Is a testing framework that its easy to setup and use.
Jest has included:
* assertions
* mocks
* spies
* stubs
* code coverage ( out of the box )

**Code sample**
```javascript
import { sum } from "utilities";

describe( "adds a with b", () => {
  const result = sum( 2, 3 );
  expect( result ).toEqual( 5 )
} );
```

**References**
* [Jest tutorial]
* [Official docs]

## Enzyme

## shallow vs mount
