## OPENING FILES:

with open('filename.txt', 'r') as file: # do something

variable 'file' is assigned a file object (iterable)

'r' - open for reading (default)

'w' - open for writing, truncating the file first

'x' - open for exclusive creation, failing if the file already exists

'a' - open for writing, appending to the end of the file if it exists

'b' - binary mode

't' - text mode (default)

'+' - open for updating (reading and writing)

## FILE OBJECT METHODS:

.read(size=-1) (Links to an external site.) This reads from the file based on the number of size bytes. If no argument is passed or None or -1 is passed, then the entire file is read.  
.readline(size=-1) (Links to an external site.) This reads at most size number of characters from the line. This continues to the end of the line and then wraps back around. If no argument is passed or None or -1 is passed, then the entire line (or rest of the line) is read.  
.readlines() (Links to an external site.) This reads the remaining lines from the file object and returns them as a list.  
.write(string) This writes the string to the file.
.writelines(seq) This writes the sequence to the file. No line endings are appended to each sequence item. It’s up to you to add the appropriate line ending(s).

### Reading and writing to file:

`with open('filename_1.txt', 'r') as file_1, open('filename_2.txt', 'r') as file_2:`  
 `for line in file_1:`  
 `file_2.write(line, end='')`

## ERRORS AND EXCEPTIONS:

Syntax error - occurs when python parser encounters incorrect syntax

Exception error - when syntactically correct Python code results in an error.

Raising an exception:

`x = 10`  
`if x > 5:`  
`raise Exception('x should not exceed 5. The value of x was: {}'.format(x))`  
`Asserting that a condition is met (otherwise AssertionError):`

`import sys`
`assert ('linux' in sys.platform), "This code runs on Linux only."`

## ERROR HANDLING:

`try: # Normal code execution`  
`except ExceptionClass[ as alias]: # Error handling part`  
`except AnoterExceptionClass[ as another_alias]: # Handle the second error`  
`else: # if the Exception isn't caught run this part`  
`finally: # run this part no matter what (e.g. close file etc)`

[Go back](./README.md)
