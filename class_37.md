## React Intro

### ES6 overview

The arrow function expression syntax is a shorter way of creating a function expression. Arrow functions do not have their own this, do not have prototypes, cannot be used for constructors, and should not be used as object methods.

ES6 introduces a shorter notation for assigning properties to variables of the same name.

    #ES5
    var obj = {
        a: a,
        b: b,
    }

    # ES6
    let obj = {
        a,
        b,
    }

The function keyword can be omitted when assigning methods on an object.

    #ES5
    var obj = {
        a: function (c, d) {},
        b: function (e, f) {},
    }

    #ES6
    let obj = {
        a(c, d) {},
        b(e, f) {},
    }

Destructuring (object matching)

    var obj = {a: 1, b: 2, c: 3}

    #ES5
    var a = obj.a
    var b = obj.b
    var c = obj.c

    #ES6
    let {a, b, c} = obj

Array iteration (looping)
var arr = ['a', 'b', 'c']

    #ES5
    for (var i = 0; i < arr.length; i++) {
        console.log(arr[i])
    }

    #ES6
    for (let i of arr) {
        console.log(i)
    }

Default parameters

    #ES5
    var func = function (a, b) {
        b = b === undefined ? 2 : b
        return a + b
    }

    #ES6
    let func = (a, b = 2) => {
        return a + b
    }

Spread syntax

    #ES6
    let arr1 = [1, 2, 3]
    let func = (a, b, c) => a + b + c

    console.log(func(...arr1)) // 6

Classes/constructor functions

    #ES5
    function Func(a, b) {
        this.a = a
        this.b = b
    }

    Func.prototype.getSum = function () {
        return this.a + this.b
    }


    #ES6
    class Func {
        constructor(a, b) {
            this.a = a
            this.b = b
        }

        getSum() {
            return this.a + this.b
        }
    }

Inheritance

    #ES6
    class Inheritance extends Func {
        constructor(a, b, c) {
            super(a, b)

            this.c = c
        }

        getProduct() {
            return this.a * this.b * this.c
        }
    }

Modules - export/import

    #index.html
    <script src="export.js"></script>
    <script type="module" src="import.js"></script>

    #export.js
    let func = (a) => a + a
    let obj = {}
    let x = 0
    export {func, obj, x}

    #import.js
    import {func, obj, x} from './export.js'
    console.log(func(3), obj, x)

Promises/Callbacks

    let doSecond = () => {
        console.log('Do second.')
    }

    let doFirst = new Promise((resolve, reject) => {
        setTimeout(() => {
            console.log('Do first.')

            resolve()
        }, 500)
    })

    doFirst.then(doSecond)

### React

**!All React components must act like pure functions with respect to their props.**

The smallest React element

    ReactDOM.render(
        <h1>Hello, world!</h1>,
        document.getElementById('root')
    );

### JSX

You can put any valid JavaScript expression inside the curly braces in JSX.

    const name = 'Josh Perez';
    const element = <h1>Hello, {name}</h1>;

    ReactDOM.render(
    element,
    document.getElementById('root')
    );

**Specifying Attributes with JSX**

_Since JSX is closer to JavaScript than to HTML, React DOM uses camelCase property naming convention instead of HTML attribute names. For example, class becomes className in JSX, and tabindex becomes tabIndex._

    const element = <div tabIndex="0"></div>;
    const element = <img src={user.avatarUrl}></img>;

If a tag is empty, you may close it immediately with />, JSX tags may contain children:

    const element = <img src={user.avatarUrl} />;
    const element = (
    <div>
        <h1>Hello!</h1>
        <h2>Good to see you here.</h2>
    </div>
    );

### React Components

Conceptually, **_components_** are like JavaScript functions. They accept arbitrary inputs (called “props”) and return React **_elements_** describing what should appear on the screen.

Simple function-based component

    function Welcome(props) {
        return <h1>Hello, {props.name}</h1>;
        }

    const element = <Welcome name="Sara" />;
    ReactDOM.render(
        element,
        document.getElementById('root')
    );

**Composing Components**

    function Welcome(props) {
        return <h1>Hello, {props.name}</h1>;
    }

    function App() {
        return (
            <div>
            <Welcome name="Sara" />
            <Welcome name="Cahal" />
            <Welcome name="Edite" />
            </div>
        );
    }

    ReactDOM.render(
        <App />,
        document.getElementById('root')
    );

**Converting function-based component into class-based:**

- Create an ES6 class, with the same name, that extends React.Component.
- Add a single empty method to it called render().
- Move the body of the function into the render() method.
- Replace props with this.props in the render() body.
- Delete the remaining empty function declaration.

        class Clock extends React.Component {
            render() {
                return (
                <div>
                    <h1>Hello, world!</h1>
                    <h2>It is {this.props.date.toLocaleTimeString()}.</h2>
                </div>
                );
            }
        }

### State

    class Clock extends React.Component {
        constructor(props) {
            super(props);
            this.state = {date: new Date()};
        }

        render() {
            return (
            <div>
                <h1>Hello, world!</h1>
                <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
            </div>
            );
        }
    }

        ReactDOM.render(
        <Clock />,
        document.getElementById('root')
    );

### Lifecycle

In applications with many components, it’s very important to free up resources taken by the components when they are destroyed. We want to set up a timer whenever the Clock is rendered to the DOM for the first time. This is called **_“mounting”_** in React. We also want to clear that timer whenever the DOM produced by the Clock is removed. This is called **_“unmounting”_** in React.

The `componentDidMount()` method runs after the component output has been rendered to the DOM. This is a good place to set up a timer:

    componentDidMount() {
        this.timerID = setInterval(
            () => this.tick(),
            1000
        );
    }

We will tear down the timer in the `componentWillUnmount()` lifecycle method:
componentWillUnmount() {
clearInterval(this.timerID);
}

### How to use state

Do Not Modify State Directly
For example, this will not re-render a component:

    // Wrong
    this.state.comment = 'Hello';

    // Correct
    this.setState({comment: 'Hello'});

Because `this.props` and `this.state` may be updated asynchronously, you should not rely on their values for calculating the next state.

    // Wrong
    this.setState({
        counter: this.state.counter + this.props.increment,
    });

    // Correct
    this.setState((state, props) => ({
        counter: state.counter + props.increment
    }));

    // Correct
    this.setState(function(state, props) {
        return {
            counter: state.counter + props.increment
        };
    });

### Handling Events
    <button onClick={activateLasers}>
        Activate Lasers
    </button>

When you define a component using an ES6 class, a common pattern is for an event handler to be a method on the class. For example, this Toggle component renders a button that lets the user toggle between “ON” and “OFF” states:

    class Toggle extends React.Component {
        constructor(props) {
            super(props);
            this.state = {isToggleOn: true};

            // This binding is necessary to make `this` work in the callback
            this.handleClick = this.handleClick.bind(this);
        }

        handleClick() {
            this.setState(state => ({
            isToggleOn: !state.isToggleOn
            }));
        }

        render() {
            return (
            <button onClick={this.handleClick}>
                {this.state.isToggleOn ? 'ON' : 'OFF'}
            </button>
            );
        }
    }

    ReactDOM.render(
        <Toggle />,
        document.getElementById('root')
    );

To make sure that `this` is bound you can use arrow function syntax
    class LoggingButton extends React.Component {
        handleClick() {
            console.log('this is:', this);
        }

        render() {
            // This syntax ensures `this` is bound within handleClick
            return (
            <button onClick={() => this.handleClick()}>
                Click me
            </button>
            );
        }
    }

### Passing Arguments to Event Handlers

    <button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
    <button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>

[Go back](./README.md)
