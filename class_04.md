## CLASSES AND OBJECTS:

Objects are an encapsulation of variables and functions into a single entity. Objects get their variables and functions from classes. Classes are essentially a template to create your objects.

### SYNTAX:

    class MyClass(ClassToInheritAfter):
    var1 = 'foo'
    var2 = 'bar'

    def my_method(self, any_parameter):
        print(any_parameter)

## RECURSION

2 biggest issues you can run into dealing with recursion:

- forget to set the base case (stack overflow error);

- forget to maintain state, i.e. pass the changing variable along with the new function call (unexpected results)

Another thing to keep in mind is that slicing actually creates a copy of the part of the list

## PYTEST FIXTURES

### SYNTAX

    @pytest.fixture
    def your_name():
    return #code goes here
    Later you can refer to it by its name (e.g. 'your_name')

As an analogy to unittest setup/teardown idea, PyTest uses fixture scope parameter as 'setup' and generators (yield statement) as 'teardown':

    @pytest.fixture
    def your_name(scope='module'):
    return #code goes here
    The code above will run only once for the entire module.

### PyTest-Cov

This (Links to an external site.) package shows you whether every part of the software was run
