## React Part II

### Conditional Rendering

In React, you can create distinct components that encapsulate behavior you need. Then, you can render only some of them, depending on the state of your application by using JavaScript operators.

You may embed expressions in JSX by wrapping them in curly braces. This includes the JavaScript logical && operator. It can be handy for conditionally including an element:

    function Mailbox(props) {
        const unreadMessages = props.unreadMessages;
        return (
            <div>
            <h1>Hello!</h1>
            {unreadMessages.length > 0 &&
                <h2>
                You have {unreadMessages.length} unread messages.
                </h2>
            }
            </div>
        );
    }

    const messages = ['React', 'Re: React', 'Re:Re: React'];

    ReactDOM.render(
        <Mailbox unreadMessages={messages} />,
        document.getElementById('root')
    );

It works because in JavaScript, `true && expression` always evaluates to expression, and `false && expression` always evaluates to false.

The same result can be achieved using ternary:

    render() {
        const isLoggedIn = this.state.isLoggedIn;
        return (
            <div>
            {isLoggedIn
                ? <LogoutButton onClick={this.handleLogoutClick} />
                : <LoginButton onClick={this.handleLoginClick} />
            }
            </div>
        );
    }

### Rendering Multiple Components

    function NumberList(props) {
        const numbers = props.numbers;
        const listItems = numbers.map((number) =>
            <li key={number.toString()}>
            {number}
            </li>
        );
        return (
            <ul>{listItems}</ul>
        );
    }

    const numbers = [1, 2, 3, 4, 5];
    ReactDOM.render(
        <NumberList numbers={numbers} />,
        document.getElementById('root')
    );

**_Keys_** help React identify which items have changed, are added, or are removed. Keys should be given to the elements inside the array to give the elements a stable identity.
Keys only make sense in the context of the surrounding array. For example, if you extract a ListItem component, you should keep the key on the `<ListItem />` elements in the array rather than on the `<li>` element in the ListItem itself.

#### Incorrect usage

    function ListItem(props) {
        const value = props.value;
        return (
            // Wrong! There is no need to specify the key here:
            <li key={value.toString()}>
            {value}
            </li>
        );
    }

    function NumberList(props) {
        const numbers = props.numbers;
        const listItems = numbers.map((number) =>
            // Wrong! The key should have been specified here:
            <ListItem value={number} />
        );
        return (
            <ul>
            {listItems}
            </ul>
        );
    }

#### Correct usage
    function ListItem(props) {
        // Correct! There is no need to specify the key here:
        return <li>{props.value}</li>;
    }

    function NumberList(props) {
        const numbers = props.numbers;
        const listItems = numbers.map((number) =>
            // Correct! Key should be specified inside the array.
            <ListItem key={number.toString()} value={number} />
        );
        return (
            <ul>
            {listItems}
            </ul>
        );
    }

A good rule of thumb is that elements inside the map() call need keys.

Keys serve as a hint to React but they don’t get passed to your components. If you need the same value in your component, pass it explicitly as a prop with a different name:

    const content = posts.map((post) =>
        <Post
            key={post.id}
            id={post.id}
            title={post.title} />
    );

### Forms
#### Controlled Components
In HTML, form elements such as `<input>`, `<textarea>`, and `<select>` typically maintain their own state and update it based on user input. In React, mutable state is typically kept in the state property of components, and only updated with `setState()`.

We can combine the two by making the React state be the “single source of truth”. Then the React component that renders a form also controls what happens in that form on subsequent user input. An input form element whose value is controlled by React in this way is called a “controlled component”.

    class NameForm extends React.Component {
        constructor(props) {
            super(props);
            this.state = {value: ''};

            this.handleChange = this.handleChange.bind(this);
            this.handleSubmit = this.handleSubmit.bind(this);
        }

        handleChange(event) {
            this.setState({value: event.target.value});
        }

        handleSubmit(event) {
            alert('A name was submitted: ' + this.state.value);
            event.preventDefault();
        }

        render() {
            return (
            <form onSubmit={this.handleSubmit}>
                <label>
                Name:
                <input type="text" value={this.state.value} onChange={this.handleChange} />
                </label>
                <input type="submit" value="Submit" />
            </form>
            );
        }
    }

#### Rendering `<select>`

    class FlavorForm extends React.Component {
        constructor(props) {
            super(props);
            this.state = {value: 'coconut'};

            this.handleChange = this.handleChange.bind(this);
            this.handleSubmit = this.handleSubmit.bind(this);
        }

        handleChange(event) {
            this.setState({value: event.target.value});
        }

        handleSubmit(event) {
            alert('Your favorite flavor is: ' + this.state.value);
            event.preventDefault();
        }

        render() {
            return (
            <form onSubmit={this.handleSubmit}>
                <label>
                Pick your favorite flavor:
                <select value={this.state.value} onChange={this.handleChange}>
                    <option value="grapefruit">Grapefruit</option>
                    <option value="lime">Lime</option>
                    <option value="coconut">Coconut</option>
                    <option value="mango">Mango</option>
                </select>
                </label>
                <input type="submit" value="Submit" />
            </form>
            );
        }
    }

You can pass an array into the value attribute, allowing you to select multiple options in a select tag:

    <select multiple={true} value={['B', 'C']}>

#### Handling Multiple Inputs
When you need to handle multiple controlled input elements, you can add a name attribute to each element and let the handler function choose what to do based on the value of `event.target.name`
    
    this.setState({
      [name]: value
    });

[Ready-to-use Form solution](https://formik.org/)

### Lifting State Up
There should be a single “source of truth” for any data that changes in a React application. Usually, the state is first added to the component that needs it for rendering. Then, if other components also need it, you can lift it up to their closest common ancestor. Instead of trying to sync the state between different components, you should rely on the top-down data flow.

Lifting state involves writing more “boilerplate” code than two-way binding approaches, but as a benefit, it takes less work to find and isolate bugs. Since any state “lives” in some component and that component alone can change it, the surface area for bugs is greatly reduced. Additionally, you can implement any custom logic to reject or transform user input.

[Go back](../README.md)
