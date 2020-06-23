## LIST COMPREHENSIONS

### BASIC SYNTAX

    [ expression for item in list if conditional ]

    e.g.

    new_list = [expression(i) for i in old_list if filter(i)]

You can also use chained for(s) in the comprehension:

    [x + y for x in [10,30,50] for y in [20,40,60]]

    >>> [30, 50, 70, 50, 70, 90, 70, 90, 110]

## DECORATORS

By definition, a decorator is a function that takes another function and extends the behavior of the latter function without explicitly modifying it.

Put simply: decorators wrap a function, **modifying its behavior**.

A simple decorator:

    def my_decorator(func):
    def wrapper():
        print("Something is happening before the function is called.")
        func()
        print("Something is happening after the function is called.")
    return wrapper

    def say_whee():
        print("Whee!")

    say_whee = my_decorator(say_whee)

Or we can use `@` symbol like this:

    def my_decorator(func):
    def wrapper():
        print("Something is happening before the function is called.")
        func()
        print("Something is happening after the function is called.")
    return wrapper

    @my_decorator
    def say_whee():
        print("Whee!")

To allow the decorator to be used with function that takes an arbitrary number of arguments, do this:

    import functools

    def do_twice(func):
        @functools.wraps(func) # Preserve introspective representation
        def wrapper_decorator(*args, **kwargs):
            # Do something before
            value = func(*args, **kwargs)
            # Do something after
            return value
        return wrapper_decorator

### EXAMPLES

Timer

    def timer(func):
    """Print the runtime of the decorated function"""
    @functools.wraps(func)
    def wrapper_timer(*args, **kwargs):
        start_time = time.perf_counter()    # 1
        value = func(*args, **kwargs)
        end_time = time.perf_counter()      # 2
        run_time = end_time - start_time    # 3
        print(f"Finished {func.__name__!r} in {run_time:.4f} secs")
        return value
    return wrapper_timer

Debug
import functools

    def debug(func):
        """Print the function signature and return value"""
        @functools.wraps(func)
        def wrapper_debug(*args, **kwargs):
            args_repr = [repr(a) for a in args]                      # 1
            kwargs_repr = [f"{k}={v!r}" for k, v in kwargs.items()]  # 2
            signature = ", ".join(args_repr + kwargs_repr)           # 3
            print(f"Calling {func.__name__}({signature})")
            value = func(*args, **kwargs)
            print(f"{func.__name__!r} returned {value!r}")           # 4
            return value
        return wrapper_debug

[Go back](./README.md)
