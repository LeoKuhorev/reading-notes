## RANDOM

### To generate a random integer in a given range:

Method 1 - using randint():

    import random
    print random.randint(0, 5)

Method 2 - using multiplication:

    import random
    random.random() * 100

### Get random value from a list:

    random.choice( ['red', 'black', 'green'] )

### Shuffle elements in a list (in place):

    from random import shuffle
    x = [[i] for i in range(10)]
    shuffle(x)

### Generate a randomly selected element from range(start, stop, step)

    random.randrange(start, stop[, step])

    import random
    for i in range(3):
        print random.randrange(0, 101, 5)

[Go back](../README.md)
