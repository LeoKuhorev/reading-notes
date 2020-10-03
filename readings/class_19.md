## Automation

### Tools

[PyAutoGUI](https://pyautogui.readthedocs.io/en/latest/) - lets your Python scripts control the mouse and keyboard to automate interactions with other applications. The API is designed to be as simple. PyAutoGUI works on Windows, macOS, and Linux, and runs on Python 2 and 3;  
[Selenium with Python](https://selenium-python.readthedocs.io/) - provides a simple API to write functional/acceptance tests using Selenium WebDriver. Through Selenium Python API you can access all functionalities of Selenium WebDriver in an intuitive way;  
[Watchdog](https://pythonhosted.org/watchdog/) - Python API library and shell utilities to monitor file system events.

[shutil](https://pymotw.com/3/shutil/) module includes high-level file operations such as copying and archiving.

### ReGex

Using `r` prefix makes the string raw (will be interpreted as-is)

    pattern = r'find_me'

`.` - A period. Matches any single character except the newline character;  
`^` - A caret. Matches the start of the string;
`$` - Matches the end of string;  
`[abc]` - Matches a or b or c;  
`[a-zA-Z0-9]` - Matches any letter from (a to z) or (A to Z) or (0 to 9);
`[^5]` - Matches any caracter that is not 5;  
`\` - (1) If the character following the backslash is a recognized escape character, then the special meaning of the term is taken; Else if the character following the `\` is not a recognized escape character, then the `\` is treated like any other character and passed through; Can also be used in front of all the metacharacters to remove their special meaning;  
`\w` - Lowercase 'w'. Matches any single letter, digit, or underscore;  
`\W` - Uppercase 'W'. Matches any character not part of `\w` (lowercase w);
`\s` - Lowercase 's'. Matches a single whitespace character like: space, newline, tab, return;  
`\S` - Uppercase 'S'. Matches any character not part of `\s` (lowercase s);  
`\d` - Lowercase d. Matches decimal digit 0-9;  
`\D` - Uppercase d. Matches any character that is not a decimal digit;  
`\t` - Lowercase t. Matches tab;  
`\n` - Lowercase n. Matches newline;  
`\r` - Lowercase r. Matches return;  
`\A` - Uppercase a. Matches only at the start of the string. Works across multiple lines as well;  
`\Z` - Uppercase z. Matches only at the end of the string;  
`\b` - Lowercase b. Matches only the beginning or end of the word;
`+` - Checks if the preceding character appears one or more times starting from that position;  
`*` - Checks if the preceding character appears zero or more times starting from that position;  
`?` - Checks if the preceding character appears exactly zero or one time starting from that position;  
`{x}` - Repeat exactly x number of times;  
`{x,}` - Repeat at least x times or more;  
`{x, y}` - Repeat at least x times but no more than y times;
`?` - Performs the match in a non-greedy or minimal fashion (as few characters as possible will be matched);

    # Greedy match (default behaviour)
    heading  = r'<h1>TITLE</h1>'
    re.match(r'<.*>', heading).group()
    >>> '<h1>TITLE</h1>'

    # Non greedy match
    heading  = r'<h1>TITLE</h1>'
    re.match(r'<.*?>', heading).group()
    >>> '<h1>'

### Python re functions

`match(pattern, string, flags=0)` - Returns a corresponding match object if zero or more characters at the beginning of string match the pattern. Else it returns None, if the string does not match the given pattern;  
`.group()` - returns the string matched by the re;

    re.search(r'Eat\tcake', 'Eat    cake').group()

    statement = 'Please contact us at: support@datacamp.com'
    match = re.search(r'([\w\.-]+)@([\w\.-]+)', statement)
    if statement:
    print('Email address:', match.group()) # The whole matched text
    print('Username:', match.group(1)) # The username (group 1)
    print('Host:', match.group(2)) # The host (group 2)

    # Named groups:
    statement = 'Please contact us at: support@datacamp.com'
    match = re.search(r'(?P<email>(?P<username>[\w\.-]+)@(?P<host>[\w\.-]+))', statement)
    if statement:
    print('Email address:', match.group('email'))
    print('Username:', match.group('username'))
    print('Host:', match.group('host'))

`start()` - Returns the starting index of the match;  
`end()` - Returns the index where the match ends;  
`span()` - Return a tuple containing the (start, end) positions of the match;  
`search(pattern, string, flags=0)` - scans through the given string/sequence, looking for the first location where the regular expression produces a match;  
_The `match()` function checks for a match only at the beginning of the string (by default), whereas the `search()` function checks for a match anywhere in the string._  
`compile(pattern, flags=0)` - If you're using the pattern multiple times it's more performant to store it as a re object:

    pattern = re.compile(r'cookie')
    sequence = 'Cake and cookie'
    pattern.search(sequence).group()

`findall(pattern, string, flags=0)` - Finds all the possible matches in the entire sequence and returns them as a list of strings. Each returned string represents one match;  
`finditer(string, [position, end_position])` - Similar to `findall()` - it finds all the possible matches in the entire sequence but returns regex match objects as an iterator;  
`sub(pattern, repl, string, count=0, flags=0)` - is the substitute function. It returns the string obtained by replacing or substituting the leftmost non-overlapping occurrences of pattern in string by the replacement repl. If the pattern is not found, then the string is returned unchanged;  
`subn(pattern, repl, string, count=0)` - returns a tuple containing the new string value and the number of replacements that were performed in the statement;  
`split(string, [maxsplit = 0])` - Splits the strings wherever the pattern matches and returns a list. If the optional argument maxsplit is nonzero, then the maximum 'maxsplit' number of splits are performed;

`IGNORECASE (I)` - Allows case-insensitive matches;  
`DOTALL (S)` - Allows . to match any character, including newline;  
`MULTILINE (M)` - Allows start of string (^) and end of string (\$) anchor to match newlines as well;  
`VERBOSE (X)` - Allows you to write whitespace and comments within a regular expression to make it more readable;

[Go back](../README.md)
