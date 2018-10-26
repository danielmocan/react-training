# Testing React Components (work-in-progress)
An important benefit of decoupling from the actual DOM implementation and working at a higher level of abstraction in JavaScript is that we can easily test React components. If you think about it, a component is not radically different than an object or a function, gets some inputs, performs some actions and returns a value (JSX in this case). 

## Jest
Since it was lanched a few years back, jest has become one of the most used testing framework, because its easy to use and setup, and has a lot of features already included in the frameworks so is not need to ad other plugins. But on ther other side is flexible and you can use it in combination with other testing utilities.

Jest has included:
* assertions
* mocks
* spies
* stubs
* code coverage

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

### Shallow
Testing a react component that do not have any children its quite easy, because its behaviour can not be affected by one of its children. But most of the react components have children. To better test components as a unit without being afected by its children Enzyme offers `shallow`.
Example
```javascript
import React from "react";
import ProductList from "./productList";
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

describe( "ProductList", () => {
    describe( "with products", () => {
        const wrapper = shallow( <ProductList list={products}/> );
        it( "renders", () => {
            expect( component.length ).toBe( 1 );
        } );

        it( "should contain two Product components", () => {
            expect( component.find("Product").length ).toEqual( 2 );
        } );
    } );
    describe( "with no products ", () => {
       const wrapper = shallow( <ProductList list={emptyList}/> );
       it( "should not find any Product component", () => {
            expect( component.find("Product").length ).toEqual( 0 );
        } );
    } );
} );
```

### Mount
There are times when we need to test a component that interacts with the DOM API, for this cases Enzyme offers us another component wrapper called `mount`. The difference between `shallow` and `mount` is that the `mount` wrapper needs to run in a browser like enviroment, mount is also known as Full DOM Rendering. As the name implies it will fully render the DOM tree of the tested component. In order to fully render the component in the tests, we have to use a library like JSDOM. JSDOM is a headless browser implementation in JS.
Luckly for us Jest has already JSDOM included, but if use another test runner with Enzyme you may have to added it to your testing setup.

As you can notice on from the example bellow (with `mount`) there is no difference.

```javascript
import React from "react";
import ProductList from "./productList";
import { mount } from "enzyme";

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

describe( "ProductList", () => {
    describe( "with products", () => {
        const wrapper = mount( <ProductList list={products}/> );
        it( "renders", () => {
            expect( component.length ).toBe( 1 );
        } );

        it( "should contain two Product components", () => {
            expect( component.find("Product").length ).toEqual( 2 );
        } );
    } );
    describe( "with no products ", () => {
       const wrapper = mount( <ProductList list={emptyList}/> );
       it( "should not find any Product component", () => {
            expect( component.find("Product").length ).toEqual( 0 );
        } );
    } );
} );
```


**References**
* [Jest tutorial](https://flaviocopes.com/jest/)
* [Jest - Official docs](https://jestjs.io/)
* [Enzyme - Official docs](https://airbnb.io/enzyme/)
* [JSDOM](https://github.com/jsdom/jsdom)
