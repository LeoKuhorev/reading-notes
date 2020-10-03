## DUNDER METHODS

`__len__` - How your class behaves when called within `len()` method;  
`__repr__` - Unambigous tring representation of the class, a generic version:

    def __repr__(self):
        return f'{self.__class__.__name__}({self.parameter_1}, {self.parameter_2})'

`__str__` - Informal srting representation for the end user;
`__getitem__` - What to return when `YourClass[i]` is called;  
`__reversed__` - What will `reversed(YourClass)` return;

Comparison operators (using `@total_ordering` allows to only specify `__eq__` and `__lt__`):

    from functools import total_ordering

    @total_ordering
    class Account:
        # ... (see above)

        def __eq__(self, other):
            return self.balance == other.balance

        def __lt__(self, other):
            return self.balance < other.balance`

`__add__` - How the class instances behave when using `+` operator:

    def __add__(self, other):
    owner = '{}&{}'.format(self.owner, other.owner)
    start_amount = self.amount + other.amount
    acc = Account(owner, start_amount)
    for t in list(self) + list(other):
        acc.add_transaction(t)
    return acc

If you want to add your object to a builtin - use `__radd__`  
`__call__` - to make instances of the class callable;

To be able to use your class with `with` (context manager) you can use `__enter__` and `__exit__`:

    class Account:
    # ... (see above)

    def __enter__(self):
        print('ENTER WITH: Making backup of transactions for rollback')
        self._copy_transactions = list(self._transactions)
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        print('EXIT WITH:', end=' ')
        if exc_type:
            self._transactions = self._copy_transactions
            print('Rolling back to previous transactions')
            print('Transaction resulted in {} ({})'.format(
                exc_type.__name__, exc_val))
        else:
            print('Transaction OK')

_! You can make your class methods return `self` - this will allow to **chain** those methods._

## Intro to Statistic

At the most basic level, _**probability**_ seeks to answer the question, “What is the chance of an event happening?” An event is some outcome of interest. To calculate the chance of an event happening, we also need to consider all the other _**events**_ that can occur.  
_**Sample space**_ - the set of all possible events that can happen

_**The Three Sigma**_ rule dictates that given a normal distribution, 68% of your observations will fall between one standard deviation of the mean. 95% will fall within two, and 99.7% will fall within three.

<div style="text-align: center"><img src="./assets/three_sigma_rule.png" style="max-width: 70%"></div>

[Go back](../README.md)
