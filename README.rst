An Introduction to Python
=========================

Note: in-class quizlets will be answered `here <https://docs.google.com/forms/d/1EsTbkRrh-E1YuXGJAXSnSby8rbXHriL5l4O5XNhm0rU/viewform>`__.

These data structures tutorials were taken from the CPython Web site
(http://www.python.org) and were then lightly edited by Titus Brown.
See `the tutorial introduction <https://docs.python.org/3.5/tutorial/introduction.html>`__ and `the data structures tutorial <https://docs.python.org/3.5/tutorial/datastructures.html>`__ for the original.

**********************************
An Informal Introduction to Python
**********************************

To run the following examples in IPython Notebook, please:

* create a new Python3 notebook;
* in that notebook, type or copy the code into cells and use Shift-ENTER
  to run them.

----

Many of the examples even those entered at the interactive
prompt, include comments.  Comments in Python start with the hash character,
``#``, and extend to the end of the physical line.  A comment may appear at the
start of a line or following whitespace or code, but not within a string
literal.  A hash character within a string literal is just a hash character.
Since comments are to clarify code and are not interpreted by Python, they may
be omitted when typing in examples.

Some examples::

   # this is the first comment
   spam = 1  # and this is the second comment
             # ... and now a third!
   text = "# This is not a comment because it's inside quotes."


.. _tut-calculator:

Using Python as a Calculator
----------------------------

Let's try some simple Python commands.


.. _tut-numbers:

Numbers
-------

The interpreter acts as a simple calculator: you can type an expression at it
and it will write the value.  Expression syntax is straightforward: the
operators ``+``, ``-``, ``*`` and ``/`` work just like in most other languages
(for example, Pascal or C); parentheses (``()``) can be used for grouping.
For example::

   >>> 2 + 2
   4
   >>> 50 - 5*6
   20
   >>> (50 - 5*6) / 4
   5.0
   >>> 8 / 5  # division always returns a floating point number
   1.6

The integer numbers (e.g. ``2``, ``4``, ``20``) have type `int`,
the ones with a fractional part (e.g. ``5.0``, ``1.6``) have type
`float`.  We will see more about numeric types later in the tutorial.

Division (``/``) always returns a float.  To do `floor division` and
get an integer result (discarding any fractional result) you can use the ``//``
operator; to calculate the remainder you can use ``%``::

   >>> 17 / 3  # classic division returns a float
   5.666666666666667
   >>>
   >>> 17 // 3  # floor division discards the fractional part
   5
   >>> 17 % 3  # the % operator returns the remainder of the division
   2
   >>> 5 * 3 + 2  # result * divisor + remainder
   17

With Python, it is possible to use the ``**`` operator to calculate powers::

   >>> 5 ** 2  # 5 squared
   25
   >>> 2 ** 7  # 2 to the power of 7
   128

The equal sign (``=``) is used to assign a value to a variable. Afterwards, no
result is displayed before the next interactive prompt::

   >>> width = 20
   >>> height = 5 * 9
   >>> width * height
   900

If a variable is not "defined" (assigned a value), trying to use it will
give you an error::

   >>> n  # try to access an undefined variable
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
   NameError: name 'n' is not defined

There is full support for floating point; operators with mixed type operands
convert the integer operand to floating point::

   >>> 3 * 3.75 / 1.5
   7.5
   >>> 7.0 / 2
   3.5

In interactive mode, the last printed expression is assigned to the variable
``_``.  This means that when you are using Python as a desk calculator, it is
somewhat easier to continue calculations, for example::

   >>> tax = 12.5 / 100
   >>> price = 100.50
   >>> price * tax
   12.5625
   >>> price + _
   113.0625
   >>> round(_, 2)
   113.06

This variable should be treated as read-only by the user.  Don't explicitly
assign a value to it --- you would create an independent local variable with the
same name masking the built-in variable with its magic behavior.

In addition to `int` and `float`, Python supports other types of
numbers, such as `~decimal.Decimal` and `~fractions.Fraction`.
Python also has built-in support for `complex numbers <typesnumeric>`,
and uses the ``j`` or ``J`` suffix to indicate the imaginary part
(e.g. ``3+5j``).


.. _tut-strings:

Strings
-------

Besides numbers, Python can also manipulate strings, which can be expressed
in several ways.  They can be enclosed in single quotes (``'...'``) or
double quotes (``"..."``) with the same result.  ``\`` can be used
to escape quotes::

   >>> 'spam eggs'  # single quotes
   'spam eggs'
   >>> 'doesn\'t'  # use \' to escape the single quote...
   "doesn't"
   >>> "doesn't"  # ...or use double quotes instead
   "doesn't"
   >>> '"Yes," he said.'
   '"Yes," he said.'
   >>> "\"Yes,\" he said."
   '"Yes," he said.'
   >>> '"Isn\'t," she said.'
   '"Isn\'t," she said.'

In the interactive interpreter, the output string is enclosed in quotes and
special characters are escaped with backslashes.  While this might sometimes
look different from the input (the enclosing quotes could change), the two
strings are equivalent.  The string is enclosed in double quotes if
the string contains a single quote and no double quotes, otherwise it is
enclosed in single quotes.  The `print` function produces a more
readable output, by omitting the enclosing quotes and by printing escaped
and special characters::

   >>> '"Isn\'t," she said.'
   '"Isn\'t," she said.'
   >>> print('"Isn\'t," she said.')
   "Isn't," she said.
   >>> s = 'First line.\nSecond line.'  # \n means newline
   >>> s  # without print(), \n is included in the output
   'First line.\nSecond line.'
   >>> print(s)  # with print(), \n produces a new line
   First line.
   Second line.

If you don't want characters prefaced by ``\`` to be interpreted as
special characters, you can use *raw strings* by adding an ``r`` before
the first quote::

   >>> print('C:\some\name')  # here \n means newline!
   C:\some
   ame
   >>> print(r'C:\some\name')  # note the r before the quote
   C:\some\name

String literals can span multiple lines.  One way is using triple-quotes:
``"""..."""`` or ``'''...'''``.  End of lines are automatically
included in the string, but it's possible to prevent this by adding a ``\`` at
the end of the line.  The following example::

   print("""\
   Usage: thingy [OPTIONS]
        -h                        Display this usage message
        -H hostname               Hostname to connect to
   """)

produces the following output (note that the initial newline is not included)::


   Usage: thingy [OPTIONS]
        -h                        Display this usage message
        -H hostname               Hostname to connect to

Strings can be concatenated (glued together) with the ``+`` operator, and
repeated with ``*``::

   >>> # 3 times 'un', followed by 'ium'
   >>> 3 * 'un' + 'ium'
   'unununium'

Two or more *string literals* (i.e. the ones enclosed between quotes) next
to each other are automatically concatenated. ::

   >>> 'Py' 'thon'
   'Python'

This only works with two literals though, not with variables or expressions::

   >>> prefix = 'Py'
   >>> prefix 'thon'  # can't concatenate a variable and a string literal
     ...
   SyntaxError: invalid syntax
   >>> ('un' * 3) 'ium'
     ...
   SyntaxError: invalid syntax

If you want to concatenate variables or a variable and a literal, use ``+``::

   >>> prefix + 'thon'
   'Python'

This feature is particularly useful when you want to break long strings::

   >>> text = ('Put several strings within parentheses '
               'to have them joined together.')
   >>> text
   'Put several strings within parentheses to have them joined together.'

Strings can be *indexed* (subscripted), with the first character having index 0.
There is no separate character type; a character is simply a string of size
one::

   >>> word = 'Python'
   >>> word[0]  # character in position 0
   'P'
   >>> word[5]  # character in position 5
   'n'

Indices may also be negative numbers, to start counting from the right::

   >>> word[-1]  # last character
   'n'
   >>> word[-2]  # second-last character
   'o'
   >>> word[-6]
   'P'

Note that since -0 is the same as 0, negative indices start from -1.

In addition to indexing, *slicing* is also supported.  While indexing is used
to obtain individual characters, *slicing* allows you to obtain substring::

   >>> word[0:2]  # characters from position 0 (included) to 2 (excluded)
   'Py'
   >>> word[2:5]  # characters from position 2 (included) to 5 (excluded)
   'tho'

Note how the start is always included, and the end always excluded.  This
makes sure that ``s[:i] + s[i:]`` is always equal to ``s``::

   >>> word[:2] + word[2:]
   'Python'
   >>> word[:4] + word[4:]
   'Python'

Slice indices have useful defaults; an omitted first index defaults to zero, an
omitted second index defaults to the size of the string being sliced. ::

   >>> word[:2]  # character from the beginning to position 2 (excluded)
   'Py'
   >>> word[4:]  # characters from position 4 (included) to the end
   'on'
   >>> word[-2:] # characters from the second-last (included) to the end
   'on'

One way to remember how slices work is to think of the indices as pointing
*between* characters, with the left edge of the first character numbered 0.
Then the right edge of the last character of a string of *n* characters has
index *n*, for example::

    +---+---+---+---+---+---+
    | P | y | t | h | o | n |
    +---+---+---+---+---+---+
    0   1   2   3   4   5   6
   -6  -5  -4  -3  -2  -1

The first row of numbers gives the position of the indices 0...6 in the string;
the second row gives the corresponding negative indices. The slice from *i* to
*j* consists of all characters between the edges labeled *i* and *j*,
respectively.

For non-negative indices, the length of a slice is the difference of the
indices, if both are within bounds.  For example, the length of ``word[1:3]`` is
2.

Attempting to use an index that is too large will result in an error::

   >>> word[42]  # the word only has 6 characters
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
   IndexError: string index out of range

However, out of range slice indexes are handled gracefully when used for
slicing::

   >>> word[4:42]
   'on'
   >>> word[42:]
   ''

Python strings cannot be changed --- they are `immutable`.
Therefore, assigning to an indexed position in the string results in an error::

   >>> word[0] = 'J'
     ...
   TypeError: 'str' object does not support item assignment
   >>> word[2:] = 'py'
     ...
   TypeError: 'str' object does not support item assignment

If you need a different string, you should create a new one::

   >>> 'J' + word[1:]
   'Jython'
   >>> word[:2] + 'py'
   'Pypy'

The built-in function `len` returns the length of a string::

   >>> s = 'supercalifragilisticexpialidocious'
   >>> len(s)
   34


.. _tut-lists:

Lists
-----

Python knows a number of *compound* data types, used to group together other
values.  The most versatile is the *list*, which can be written as a list of
comma-separated values (items) between square brackets.  Lists might contain
items of different types, but usually the items all have the same type. ::

   >>> squares = [1, 4, 9, 16, 25]
   >>> squares
   [1, 4, 9, 16, 25]

Like strings (and all other built-in `sequence` type), lists can be
indexed and sliced::

   >>> squares[0]  # indexing returns the item
   1
   >>> squares[-1]
   25
   >>> squares[-3:]  # slicing returns a new list
   [9, 16, 25]

All slice operations return a new list containing the requested elements.  This
means that the following slice returns a new (shallow) copy of the list::

   >>> squares[:]
   [1, 4, 9, 16, 25]

Lists also support operations like concatenation::

   >>> squares + [36, 49, 64, 81, 100]
   [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]

Unlike strings, which are `immutable`, lists are a `mutable`
type, i.e. it is possible to change their content::

    >>> cubes = [1, 8, 27, 65, 125]  # something's wrong here
    >>> 4 ** 3  # the cube of 4 is 64, not 65!
    64
    >>> cubes[3] = 64  # replace the wrong value
    >>> cubes
    [1, 8, 27, 64, 125]

You can also add new items at the end of the list, by using
the `~list.append` *method* (we will see more about methods later)::

   >>> cubes.append(216)  # add the cube of 6
   >>> cubes.append(7 ** 3)  # and the cube of 7
   >>> cubes
   [1, 8, 27, 64, 125, 216, 343]

Assignment to slices is also possible, and this can even change the size of the
list or clear it entirely::

   >>> letters = ['a', 'b', 'c', 'd', 'e', 'f', 'g']
   >>> letters
   ['a', 'b', 'c', 'd', 'e', 'f', 'g']
   >>> # replace some values
   >>> letters[2:5] = ['C', 'D', 'E']
   >>> letters
   ['a', 'b', 'C', 'D', 'E', 'f', 'g']
   >>> # now remove them
   >>> letters[2:5] = []
   >>> letters
   ['a', 'b', 'f', 'g']
   >>> # clear the list by replacing all the elements with an empty list
   >>> letters[:] = []
   >>> letters
   []

The built-in function `len` also applies to lists::

   >>> letters = ['a', 'b', 'c', 'd']
   >>> len(letters)
   4

It is possible to nest lists (create lists containing other lists), for
example::

   >>> a = ['a', 'b', 'c']
   >>> n = [1, 2, 3]
   >>> x = [a, n]
   >>> x
   [['a', 'b', 'c'], [1, 2, 3]]
   >>> x[0]
   ['a', 'b', 'c']
   >>> x[0][1]
   'b'

.. _tut-firststeps:

Data Structures
---------------

This section describes some things you've learned about already in more detail,
and adds some new things as well.

More on Lists
-------------

The list data type has some more methods.  Here are all of the methods of list
objects::


   list.append(x)

      Add an item to the end of the list.  Equivalent to ``a[len(a):] = [x]``.

   list.extend(L)

   Extend the list by appending all the items in the given list.  Equivalent to
   ``a[len(a):] = L``.


   list.insert(i, x)

   Insert an item at a given position.  The first argument is the index of the
   element before which to insert, so ``a.insert(0, x)`` inserts at the front of
   the list, and ``a.insert(len(a), x)`` is equivalent to ``a.append(x)``.


   list.remove(x)

   Remove the first item from the list whose value is *x*.  It is an error if
   there is no such item.


   list.pop([i])

     Remove the item at the given position in the list, and return it.  If no index
     is specified, ``a.pop()`` removes and returns the last item in the list.  (The
     square brackets around the *i* in the method signature denote that the parameter
     is optional, not that you should type square brackets at that position.  You
     will see this notation frequently in the Python Library Reference.)


   list.clear()

      Remove all items from the list.  Equivalent to ``del a[:]``.


   list.index(x)

   Return the index in the list of the first item whose value is *x*. It is an
   error if there is no such item.


   list.count(x)

   Return the number of times *x* appears in the list.


   list.sort(key=None, reverse=False)

   Sort the items of the list in place (the arguments can be used for sort
   customization, see `sorted` for their explanation).


   list.reverse()

   Reverse the elements of the list in place.

   list.copy()

   Return a shallow copy of the list.  Equivalent to ``a[:]``.


An example that uses most of the list methods::

   >>> a = [66.25, 333, 333, 1, 1234.5]
   >>> print(a.count(333), a.count(66.25), a.count('x'))
   2 1 0
   >>> a.insert(2, -1)
   >>> a.append(333)
   >>> a
   [66.25, 333, -1, 333, 1, 1234.5, 333]
   >>> a.index(333)
   1
   >>> a.remove(333)
   >>> a
   [66.25, -1, 333, 1, 1234.5, 333]
   >>> a.reverse()
   >>> a
   [333, 1234.5, 1, 333, -1, 66.25]
   >>> a.sort()
   >>> a
   [-1, 1, 66.25, 333, 333, 1234.5]
   >>> a.pop()
   1234.5
   >>> a
   [-1, 1, 66.25, 333, 333]

You might have noticed that methods like ``insert``, ``remove`` or
``sort`` that only modify the list have no return value printed --
they return the default ``None``. This is a design principle for
all mutable data structures in Python.


.. _tut-lists-as-stacks:

The `del` statement
-------------------

There is a way to remove an item from a list given its index instead of its
value: the `del` statement.  This differs from the `pop` method
which returns a value.  The `del` statement can also be used to remove
slices from a list or clear the entire list (which we did earlier by assignment
of an empty list to the slice).  For example::

   >>> a = [-1, 1, 66.25, 333, 333, 1234.5]
   >>> del a[0]
   >>> a
   [1, 66.25, 333, 333, 1234.5]
   >>> del a[2:4]
   >>> a
   [1, 66.25, 1234.5]
   >>> del a[:]
   >>> a
   []

`del` can also be used to delete entire variables::

   >>> del a

Referencing the name ``a`` hereafter is an error (at least until another value
is assigned to it).  We'll find other uses for `del` later.


.. _tut-tuples:

Tuples and Sequences
--------------------

We saw that lists and strings have many common properties, such as indexing and
slicing operations.  They are two examples of *sequence* data types (see
`typesseq`).  Since Python is an evolving language, other sequence data
types may be added.  There is also another standard sequence data type: the
*tuple*.

A tuple consists of a number of values separated by commas, for instance::

   >>> t = 12345, 54321, 'hello!'
   >>> t[0]
   12345
   >>> t
   (12345, 54321, 'hello!')
   >>> # Tuples may be nested:
   ... u = t, (1, 2, 3, 4, 5)
   >>> u
   ((12345, 54321, 'hello!'), (1, 2, 3, 4, 5))
   >>> # Tuples are immutable:
   ... t[0] = 88888
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
   TypeError: 'tuple' object does not support item assignment
   >>> # but they can contain mutable objects:
   ... v = ([1, 2, 3], [3, 2, 1])
   >>> v
   ([1, 2, 3], [3, 2, 1])


As you see, on output tuples are always enclosed in parentheses, so that nested
tuples are interpreted correctly; they may be input with or without surrounding
parentheses, although often parentheses are necessary anyway (if the tuple is
part of a larger expression).  It is not possible to assign to the individual
items of a tuple, however it is possible to create tuples which contain mutable
objects, such as lists.

Though tuples may seem similar to lists, they are often used in different
situations and for different purposes.
Tuples are `immutable`, and usually contain an heterogeneous sequence of
elements that are accessed via unpacking (see later in this section) or indexing
(or even by attribute in the case of `namedtuples <collections.namedtuple>`).
Lists are `mutable`, and their elements are usually homogeneous and are
accessed by iterating over the list.

A special problem is the construction of tuples containing 0 or 1 items: the
syntax has some extra quirks to accommodate these.  Empty tuples are constructed
by an empty pair of parentheses; a tuple with one item is constructed by
following a value with a comma (it is not sufficient to enclose a single value
in parentheses). Ugly, but effective.  For example::

   >>> empty = ()
   >>> singleton = 'hello',    # <-- note trailing comma
   >>> len(empty)
   0
   >>> len(singleton)
   1
   >>> singleton
   ('hello',)

The statement ``t = 12345, 54321, 'hello!'`` is an example of *tuple packing*:
the values ``12345``, ``54321`` and ``'hello!'`` are packed together in a tuple.
The reverse operation is also possible::

   >>> x, y, z = t

This is called, appropriately enough, *sequence unpacking* and works for any
sequence on the right-hand side.  Sequence unpacking requires that there are as
many variables on the left side of the equals sign as there are elements in the
sequence.  Note that multiple assignment is really just a combination of tuple
packing and sequence unpacking.


.. _tut-sets:

Sets
----

Python also includes a data type for *sets*.  A set is an unordered collection
with no duplicate elements.  Basic uses include membership testing and
eliminating duplicate entries.  Set objects also support mathematical operations
like union, intersection, difference, and symmetric difference.

Curly braces or the `set` function can be used to create sets.  Note: to
create an empty set you have to use ``set()``, not ``{}``; the latter creates an
empty dictionary, a data structure that we discuss in the next section.

Here is a brief demonstration::

   >>> basket = {'apple', 'orange', 'apple', 'pear', 'orange', 'banana'}
   >>> print(basket)                      # show that duplicates have been removed
   {'orange', 'banana', 'pear', 'apple'}
   >>> 'orange' in basket                 # fast membership testing
   True
   >>> 'crabgrass' in basket
   False

   >>> # Demonstrate set operations on unique letters from two words
   ...
   >>> a = set('abracadabra')
   >>> b = set('alacazam')
   >>> a                                  # unique letters in a
   {'a', 'r', 'b', 'c', 'd'}
   >>> a - b                              # letters in a but not in b
   {'r', 'd', 'b'}
   >>> a | b                              # letters in either a or b
   {'a', 'c', 'r', 'd', 'b', 'm', 'z', 'l'}
   >>> a & b                              # letters in both a and b
   {'a', 'c'}
   >>> a ^ b                              # letters in a or b but not both
   {'r', 'd', 'b', 'm', 'z', 'l'}

Similarly to `list comprehensions <tut-listcomps>`, set comprehensions
are also supported::

   >>> a = {x for x in 'abracadabra' if x not in 'abc'}
   >>> a
   {'r', 'd'}


.. _tut-dictionaries:

Dictionaries
------------

Another useful data type built into Python is the *dictionary* (see
`typesmapping`). Dictionaries are sometimes found in other languages as
"associative memories" or "associative arrays".  Unlike sequences, which are
indexed by a range of numbers, dictionaries are indexed by *keys*, which can be
any immutable type; strings and numbers can always be keys.  Tuples can be used
as keys if they contain only strings, numbers, or tuples; if a tuple contains
any mutable object either directly or indirectly, it cannot be used as a key.
You can't use lists as keys, since lists can be modified in place using index
assignments, slice assignments, or methods like `append` and
`extend`.

It is best to think of a dictionary as an unordered set of *key: value* pairs,
with the requirement that the keys are unique (within one dictionary). A pair of
braces creates an empty dictionary: ``{}``. Placing a comma-separated list of
key:value pairs within the braces adds initial key:value pairs to the
dictionary; this is also the way dictionaries are written on output.

The main operations on a dictionary are storing a value with some key and
extracting the value given the key.  It is also possible to delete a key:value
pair with ``del``. If you store using a key that is already in use, the old
value associated with that key is forgotten.  It is an error to extract a value
using a non-existent key.

Performing ``list(d.keys())`` on a dictionary returns a list of all the keys
used in the dictionary, in arbitrary order (if you want it sorted, just use
``sorted(d.keys())`` instead). To check whether a single key is in the
dictionary, use the `in` keyword.

Here is a small example using a dictionary::

   >>> tel = {'jack': 4098, 'sape': 4139}
   >>> tel['guido'] = 4127
   >>> tel
   {'sape': 4139, 'guido': 4127, 'jack': 4098}
   >>> tel['jack']
   4098
   >>> del tel['sape']
   >>> tel['irv'] = 4127
   >>> tel
   {'guido': 4127, 'irv': 4127, 'jack': 4098}
   >>> list(tel.keys())
   ['irv', 'guido', 'jack']
   >>> sorted(tel.keys())
   ['guido', 'irv', 'jack']
   >>> 'guido' in tel
   True
   >>> 'jack' not in tel
   False

The `dict` constructor builds dictionaries directly from sequences of
key-value pairs::

   >>> dict([('sape', 4139), ('guido', 4127), ('jack', 4098)])
   {'sape': 4139, 'jack': 4098, 'guido': 4127}

In addition, dict comprehensions can be used to create dictionaries from
arbitrary key and value expressions::

   >>> {x: x**2 for x in (2, 4, 6)}
   {2: 4, 4: 16, 6: 36}

When the keys are simple strings, it is sometimes easier to specify pairs using
keyword arguments::

   >>> dict(sape=4139, guido=4127, jack=4098)
   {'sape': 4139, 'jack': 4098, 'guido': 4127}


.. _tut-loopidioms:

More on Conditions
------------------

The conditions used in ``while`` and ``if`` statements can contain any
operators, not just comparisons.

The comparison operators ``in`` and ``not in`` check whether a value occurs
(does not occur) in a sequence.  The operators ``is`` and ``is not`` compare
whether two objects are really the same object; this only matters for mutable
objects like lists.  All comparison operators have the same priority, which is
lower than that of all numerical operators.

Comparisons can be chained.  For example, ``a < b == c`` tests whether ``a`` is
less than ``b`` and moreover ``b`` equals ``c``.

Comparisons may be combined using the Boolean operators ``and`` and ``or``, and
the outcome of a comparison (or of any other Boolean expression) may be negated
with ``not``.  These have lower priorities than comparison operators; between
them, ``not`` has the highest priority and ``or`` the lowest, so that ``A and
not B or C`` is equivalent to ``(A and (not B)) or C``. As always, parentheses
can be used to express the desired composition.

The Boolean operators ``and`` and ``or`` are so-called *short-circuit*
operators: their arguments are evaluated from left to right, and evaluation
stops as soon as the outcome is determined.  For example, if ``A`` and ``C`` are
true but ``B`` is false, ``A and B and C`` does not evaluate the expression
``C``.  When used as a general value and not as a Boolean, the return value of a
short-circuit operator is the last evaluated argument.

It is possible to assign the result of a comparison or other Boolean expression
to a variable.  For example, ::

   >>> string1, string2, string3 = '', 'Trondheim', 'Hammer Dance'
   >>> non_null = string1 or string2 or string3
   >>> non_null
   'Trondheim'

Note that in Python, unlike C, assignment cannot occur inside expressions. C
programmers may grumble about this, but it avoids a common class of problems
encountered in C programs: typing ``=`` in an expression when ``==`` was
intended.


.. _tut-comparing:

Next lessons
------------

(These are a subset of the Data Carpentry python-for-ecologists
lessons, `available here <http://www.datacarpentry.org/python-ecology/>`__.)

`Starting with Data (DataFrames and Pandas) <https://github.com/ngs-docs/2015-python-intro/blob/master/01-starting-with-data.md>`__

`Indexing, Slicing, and Subsetting DataFrames in Python <https://github.com/ngs-docs/2015-python-intro/blob/master/02-index-slice-subset.md>`__

`Plotting with matplotlib <https://github.com/ngs-docs/2015-python-intro/blob/master/06-plotting-with-matplotlib.md>`__

More resources
--------------

Some books you should look into --

1. `Practical Computing for Biologists <http://practicalcomputing.org/>`__

2. `Bioinformatics Data Skills <http://shop.oreilly.com/product/0636920030157.do>`__
