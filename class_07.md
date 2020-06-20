## SCOPE

**_LEGB:_**  
**Local** scope is the code block or body of any Python function or lambda expression. It’s created at function call, not at function definition, so if a function called multiple times or recursively, each call will create a new scope;  
**Enclosing** scope only exists for nested functions. If the local scope is an inner or nested function, then the enclosing scope is the scope of the outer or enclosing function;  
**Global** scope is the top-most scope in a Python program, script, or module. This Python scope contains all of the names that you define at the top level of a program or a module;  
**Built-in** scope is created or loaded whenever you run a script or open an interactive session. This scope contains names such as keywords, functions, exceptions, and other attributes that are built into Python.

This is how namespace lookup works:

    for scope in LEGB:
        if name in scope:
            return name
    raise NameError(f'name {name} is not defined')

Python scopes are implemented as dictionaries that map names to objects. These dictionaries are commonly called **_namespaces_**. To access namespase you can call `.__dict__` on the object.

- `dir()` - gives you a list of names in global scope;
- `globals()` - returns a dict with global namespace;
- `locals()` - when called within a function returns a dict with local namespace;
- `vars()` is a Python built-in function that returns the `.__dict__`attribute of a module, class, instance, or any other object which has a dictionary attribute.

You can access global or enclosing variables from the inner scope, but you can't edit them. To do so you need to use `global` and `nonlocal` statements, e.g.

var = 1
def add_one():
global var
var += 1
add_one()
print(var) # 2

    def outer():
        var = 1
        def inner()
            nonlocal var
            var += 1
        inner()
        print(var) # 2

### CLASS SCOPE

In general, when you’re writing object-oriented code in Python and you try to access an attribute, your program takes the following steps:

Check the instance local scope or namespace first.
If the attribute is not found there, then check the class local scope or namespace.
If the name doesn’t exist in the class namespace either, then you’ll get an AttributeError.

    class A:
        var = 100
        def __init__(self):
            self.var = 200

        def access_attr(self):
            print(f'The instance attribute is: {self.var}')
            print(f'The class attribute is: {A.var}')

    obj = A()
    obj.access_attr()
    # The instance attribute is: 200
    # The class attribute is: 100

### CLOSURES

When you handle a nested function as data, the statements that make up that function are packaged together with the environment in which they execute. The resulting object is known as a closure.

    def power_factory(exp):
        def power(base):
            return base ** exp
        return power

    square = power_factory(2)
    square(10) # 100
    cube = power_factory(3)
    cube(10) # 1000

A closure is an inner or nested function that carries information about its enclosing scope, even though this scope has completed its execution.

Use of closures in standart pythin library:

    from functools import partial
    def power(exp, base):
        return base ** exp

    square = partial(power, 2)
    square(10) # 100

[Go back](./README.md)
