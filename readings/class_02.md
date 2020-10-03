## IMPORTING MODULES:

If the DIR is in the PATH - just

'import module_name'
DIR can be appended to the PATH, bu easier just to refer to it using relative or absolute path:

'from path/to/the/dir import module_name as alias' or

'from path/to/the/dir/module_name import function_name, function2_name' etc

Run as a script:

    python -m game_of_greed.game

Run as a module:

    PYTHONPATH=‘.’ python game_of_greed/game.py

## PYTEST:

In it's most basic form the workflow is:

- create test_module_name.py;

- import a module/function you need to test;

- create test_function_name() function and set the expected result

- use 'assert' statement to make sure that the actual function return == to the expected result

- VSCode has great test suites support

## RECURSION:

- find the base case (when the recursion stops) - otherwise, stack overflows;

- find recursive case (keep calling the function until it hits the base case)

Can always be replaced with iterative solution, but is much easier to read in some examples (tree traversing etc).

[Go back](../README.md)
