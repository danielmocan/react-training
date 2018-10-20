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
Is a JavaScript testing library for React developed by Airbnb. Enzyme API is easy to use and is very similar to jQuery's API for DOM manipulation and traversal.
To test React components, most of the times you will choose from `shallow` and `mount`.
Testing a react component that do not have any children its quite easy, because its behaviour can not be affected by one of its children. But most of the react components have children. To better test components as a unit without being afected by its children Enzyme offers `shallow`.
Example
```javascript
import React from "react";
import ProductsList from "./productsList";
import { shallow } from "enzyme";

const products = [
  {
    name: "Bread",
    price: "$2"
  },
  {
    name: "Butter",
    price: "$4"
  }
];

const emptyList = [];

describe( "ProductsList", () => {
    describe( "with products", () => {
        const wrapper = shallow( <ProductsList list={products}/> );
        it( "renders", () => {
            expect( component.length ).toBe( 1 );
        } );

        it( "should contain two Product components", () => {
            expect( component.find("Product").length ).toEqual( 2 );
        } );
    } );
    describe( "with no products ", () => {
       const wrapper = shallow( <ProductsList list={emptyList}/> );
       it( "should not find any Product component", () => {
            expect( component.find("Product").length ).toEqual( 0 );
        } );
    } );
} );
```

## shallow vs mount
