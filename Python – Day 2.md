# Python Study Notes – Day 2

Nov 19, 2026 · @Soni Sindhal

## Day 2 – Strings and Lists (Session 2)

### What a string is

Anything written between single quotes `'...'` or double quotes `"..."` is a string. A string is used to store text, such as a name. Python treats a string as a **sequence**: it keeps track of every character in order, which is what lets you pick out a letter by its position later on.

> **In plain words:** a string is a **necklace of letter beads**. Each bead is one character, and the beads sit in a fixed order. Anything in quote marks becomes a necklace, even a number like `'5'`. It is then just the picture of a 5, not a number you can add up.

A string does not define a data type for what is inside it. Everything between the quotes is just text, so the whole thing is **one single value of type `str`**, even if it contains numbers.

```python
s = 'hello joey 445efddu43 0.5'
print(type(s))
print(len(s))
```

Output:

```text
<class 'str'>
25
```

The `0.5` at the end is not a float, and `445efddu43` is not a number mixed with a word. Python does not split a string into parts that each have their own type. All 25 characters, digits included, are text, so the whole string is one `str` value. Python has no separate `varchar` type, because that is a database term.

Digits inside quotes behave like text, not like numbers:

```python
print('0.5' + '1')              # text joined to text
print(0.5 + 1)                  # float plus int
print(float('0.5') + 1)         # convert the text to a float first
print(type('0.5'), type(0.5))
```

Output:

```text
0.51
1.5
1.5
<class 'str'> <class 'float'>
```

If you need the number inside a string, convert it with `float()` or `int()`, as in type casting on Day 1.

### Mutable and immutable

Mutability and immutability are two properties of data types (not functions):

- **Mutable:** the object can be changed after it is created.
- **Immutable:** once the object is created, what is inside it cannot be changed.

**A string is immutable.** You can read any character, but you can't replace one:

```python
s = 'Hello world'
s[0] = 'x'
```

Output:

```text
TypeError: 'str' object does not support item assignment
```

Python tells you directly that you can't assign to an item of a string.

> **In plain words:** immutable means "can't be changed after it is made", like something written in pen. You can't swap one letter inside a string. You can only make a *new* string.

What you can do is build a **new** string, for example by joining strings with `+`. That is covered under **Concatenating strings** below. Lists are the mutable type, and they come later in this session.

### PS: `\n` prints a new line

Inside a string, `\n` (a **backslash** followed by `n`, not a forward slash) means "start a new line here". Everything after it is printed on the next line.

```python
print('Hello World 1\nHello World 2')
print('Use \n to print a new line')
print('\n')
print('See what I mean?')
```

Output:

```text
Hello World 1
Hello World 2
Use 
 to print a new line


See what I mean?
```

In the third line, `print('\n')` prints an empty line, and `print` adds its own line break as well, so you see two blank lines in total.

### Indexing

Because a string is a sequence, every character has a position called its **index**. Put the index in square brackets after the string to get the character at that position. Counting starts at **0**, so the first character is `s[0]`.

> **In plain words:** every bead has a **seat number**, and the numbering starts at **0**, not 1. `s[0]` means "who is in seat 0?" (the first character). `s[-1]` means "the last seat", counting back from the end.

The string `'Hello World'` has 11 characters, including the space:

| Character | H | e | l | l | o | (space) | W | o | r | l | d |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
| Negative index | -11 | -10 | -9 | -8 | -7 | -6 | -5 | -4 | -3 | -2 | -1 |

`s[1]` gives you the **character** at that position, not the position number.

```python
s = 'Hello World'
print(s[0])
print(s[1])
print(s[10])
```

Output:

```text
H
e
d
```

The last valid index is `len(s) - 1`, which is 10 here. An index past the end gives an error:

```python
print(s[11])
```

Output:

```text
IndexError: string index out of range
```

### Slicing

Slicing takes a part of the string, not just one character. The format is `s[start:stop:step]`, which is the same three parameters as `range()`:

- **start:** where to begin (included). The default is 0.
- **stop:** where to end (**not included**). The default is the end of the string.
- **step:** how many positions to jump each time. The default is 1.

Any of the three can be left out. The colons stay.

> **In plain words:** slicing is **cutting a piece out of the necklace**. `s[1:4]` means "start at seat 1 and stop *before* seat 4". The step is how many seats you jump each time, and a step of `-1` reads the necklace backwards.

**Start and stop:**

```python
print(s[1:])      # from index 1 to the end
print(s[:5])      # from the start up to, but not including, index 5
print(s[::])      # everything
print(s[0:1])     # index 0 only, which gives a single character
```

Output:

```text
ello World
Hello
Hello World
H
```

`s[1:]` starts at index 1, the second character. `s[:5]` ends at index 4, because index 5 is not included. `s[0:1]` is just index 0 because it stops before 1.

**Negative numbers count from the end.** `-1` is the last character, `-2` the one before it, and so on:

```python
print(s[-3])      # third character from the end
print(s[:-1])     # everything except the last character
```

Output:

```text
r
Hello Worl
```

A negative index doesn't reverse the string. It only changes where you start counting from.

**Step size:**

```python
print(s[::2])     # every 2nd character
print(s[::-1])    # step of -1 goes backwards, so the string is reversed
```

Output:

```text
HloWrd
dlroW olleH
```

It is the **negative step** that reverses the string, as it does in `range()`.

**All three together.** Start at index 1, stop before index 9, take every 3rd character (indexes 1, 4 and 7):

```python
print(s[1:9:3])
```

Output:

```text
eoo
```

Slicing makes a new string, so the original is unchanged:

```python
print(s)
```

Output:

```text
Hello World
```

### Concatenating strings

The `+` sign joins strings together. It always creates a **new** string. It never changes the original, because strings are immutable.

```python
s = "hello world"
print(s + " I am Joey")
print(s)
```

Output:

```text
hello world I am Joey
hello world
```

The first line shows the joined result. The second shows that `s` itself is still only `hello world`. This is what proves a string is immutable: the `+` made a new string, and `s` was not touched. The new string was printed and then thrown away.

> **In plain words:** `+` is **glue**. It sticks two strings together into a new one, and the old strings are left as they were. The new string has no name until you give it one, so write `s = s + '!'` to keep it.

**To keep the change, reassign.** Join the strings and store the result back in the same variable:

```python
s = "hello world"
s = s + " I am Joey"
print(s)
```

Output:

```text
hello world I am Joey
```

The old string is not edited. The name `s` now points at the new, longer string.

Note that the space in `" I am Joey"` has to be typed inside the quotes. `+` adds nothing between the two strings by itself.

`+` only joins a string to another string. To add a number, convert it first with `str()`:

```python
print("age: " + str(5))
print("age: " + 5)
```

Output:

```text
age: 5
TypeError: can only concatenate str (not "int") to str
```

### Repeating a string with `*`

Multiplying a string by a whole number repeats it that many times. In the notebook the example is a single letter, `letter = 'z'`:

```python
letter = 'z'
print(letter * 5)
print(letter * 100)
print(len(letter * 100))
```

Output:

```text
zzzzz
zzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzz
100
```

`letter * 100` gives the letter `z` printed 100 times in a row, as one string that is 100 characters long. It works for longer strings too:

```python
print('ab' * 3)
```

Output:

```text
ababab
```

**About `letter = "2"`.** The notebook's example is the letter `z`, not the digit 2, so that was most likely the letter `z`. If it were the digit in quotes, it would still be text, so `'2' * 3` repeats the character instead of doing maths:

```python
print('2' * 3)
print(2 * 3)
```

Output:

```text
222
6
```

The result of `letter * 100` is also the same letter repeated, not a single `Z`. A capital `'Z' * 100` would give capital Zs.

### String methods: upper() and lower()

A **method** is a function that belongs to an object. You call it with a dot after the object, then the method name, then brackets: `object.method(parameters)`. The brackets are always needed, even when there is nothing inside them, so write `s.upper()` and not `s.upper`.

> **In plain words:** a method is a **built-in button** that every string comes with. You press it by writing a dot, the button's name and brackets, for example `s.upper()`. The string doesn't change. You get a new result back.

`upper()` gives the string in uppercase and `lower()` gives it in lowercase. Strings are immutable, so a method never changes `s`. It gives you a new string.

```python
s = 'Hello world'
print(s.upper())
print(s.lower())
print(s)
```

Output:

```text
HELLO WORLD
hello world
Hello world
```

### split()

`split()` cuts a string into pieces and gives them back as a **list** (in square brackets). With nothing inside the brackets it splits at the spaces, so each word becomes one item. If you give it a character, it cuts at every place that character appears, and the character itself is **removed** from the result.

> **In plain words:** `split` is **cutting a cake into slices**. You say where to cut, and you get a list of the slices. The knife mark itself (the separator) disappears.

```python
s = 'Hello world'
print(s.split())
print(s.split('w'))
print(s.split('o'))
```

Output:

```text
['Hello', 'world']
['Hello ', 'orld']
['Hell', ' w', 'rld']
```

In `s.split('w')` the `w` is gone and the text before and after it becomes two items. Split at `'o'` gives three items, because there are two `o`s.

You can limit the number of cuts with a second value. `split('o', 1)` cuts only at the first `o`:

```python
print('hello world python'.split('o', 1))
```

Output:

```text
['hell', ' world python']
```

**Splitting a name at the dot.** Splitting at `'.'` gives the parts as a list. You then pick a part by its index. Index `0` is the first, and `-1` is the last:

```python
x = 'Soni.Sindhal'
r = x.split('.')
print(r)
print(r[0])
print(r[-1])
```

Output:

```text
['Soni', 'Sindhal']
Soni
Sindhal
```

You don't subtract anything from the string. `x - x.split('.')` is not valid, because `-` doesn't work on strings. It gives `TypeError: unsupported operand type(s) for -: 'str' and 'int'`. The result of `split` is stored in `r`, and you index `r`.

### Location and counting: count() and find()

- **`count(x)`** tells you how many times `x` appears in the string.
- **`find(x)`** gives the index of the **first** place `x` appears. If it isn't there, it gives `-1`.

What you search for must be a string, so put it in quotes. `s.count(0)` with a number fails, while `s.count('0')` counts the character zero.

```python
s = 'Hello world'
print(s.count('l'))
print(s.count('o'))
print(s.find('o'))
print(s.find('z'))
```

Output:

```text
3
2
4
-1
```

There are three `l`s and two `o`s. The first `o` is at index 4. There is no `z`, so `find` gives `-1`.

`find` can also take a start and an end position, so it only looks in that part of the string:

```python
text = "apple, banana, apple"
print(text.find("apple"))         # first apple
print(text.find("apple", 5))      # start looking at index 5
print(text.find("apple", 5, 14))  # only look between index 5 and 14
```

Output:

```text
0
15
-1
```

Starting from index 5 skips the first `apple`, so it finds the second one at 15. Between indexes 5 and 14 there is only `, banana,`, so it isn't found and gives `-1`.

### expandtabs()

`\t` (a **backslash** followed by `t`, not `/t`) means a tab, a wide gap. `expandtabs()` turns each tab into spaces. Without a number the tab stops are 8 characters apart. A number inside the brackets sets a different width.

```python
print('a\tb')
print('a\tb'.expandtabs())
print('a\tb'.expandtabs(4))
```

Output:

```text
a	b
a       b
a   b
```

The first line prints the real tab. The second pads `a` with spaces up to the next multiple of 8, and the third up to the next multiple of 4.

### The is... check methods

These methods look at the whole string and give back `True` or `False`. The names have no underscores (`isalnum`, not `is_alnum`), and you call them with brackets.

| Method | Gives `True` when | Example | Result |
| --- | --- | --- | --- |
| `isalnum()` | every character is a letter or a digit | `'hello5'.isalnum()` | True |
| `isalpha()` | every character is a letter | `'Ruchik'.isalpha()` | True |
| `isnumeric()` | every character is a digit | `'5'.isnumeric()` | True |
| `islower()` | every letter is lowercase | `'ruch'.islower()` | True |
| `isupper()` | every letter is uppercase | `'RUCH'.isupper()` | True |
| `istitle()` | each word starts with a capital and the rest are lowercase | `'Hello World'.istitle()` | True |
| `isspace()` | the string contains only spaces (whitespace) | `' '.isspace()` | True |
| `endswith(x)` | the string ends with `x` | `'hello'.endswith('o')` | True |

```python
print('hello'.isalnum())
print('$'.isalnum())
print('Ruchik'.isalpha())
print('ruchik5'.isalpha())
print('5'.isnumeric())
print('ruch'.islower())
print('RUCH'.isupper())
print('Ruchik'.istitle())
print('Hello world'.istitle())
print(' '.isspace())
print('hello'.endswith('o'))
```

Output:

```text
True
False
True
False
True
True
True
True
False
True
True
```

`'$'` is not letters or digits, so `isalnum()` is False. `'ruchik5'` has a digit, so `isalpha()` is False. `'Hello world'` has a lowercase `w` at the start of the second word, so `istitle()` is False. `endswith('o')` does the same job as checking whether the last character is `'o'`.

> **In plain words:** the `is...` methods are **yes/no questions** about the text ("is it all letters?", "is it all small letters?"). The answer is always `True` or `False`.

### partition()

`partition(x)` also cuts a string at `x`, but it behaves differently from `split`:

|  | `split(x)` | `partition(x)` |
| --- | --- | --- |
| Cuts at | every `x` | only the **first** `x` |
| Separator `x` | removed | **kept** as the middle item |
| Gives back | a list of all the pieces | a tuple of 3 items: before, separator, after |

```python
s = 'hello'
print(s.partition('e'))
print(s.split('e'))
```

Output:

```text
('h', 'e', 'llo')
['h', 'llo']
```

`partition('e')` gives `h`, then `e`, then `llo`, so you keep the separator and all the text. `split('e')` drops the `e`.

> **In plain words:** `partition` cuts only **once**, at the first mark, and always gives exactly three pieces: the left part, the mark itself, and the right part.

With more than one match, `partition` stops at the first and `split` cuts at all of them:

```python
print('hello world'.partition('o'))
print('hello world'.split('o'))
```

Output:

```text
('hell', 'o', ' world')
['hell', ' w', 'rld']
```

If the separator isn't in the string, `partition` gives the whole string followed by two empty strings:

```python
print('hello'.partition('z'))
```

Output:

```text
('hello', '', '')
```

# Lists

A **list** is a sequence like a string, but it is **mutable** (its items can be changed) and it can hold **any kind of data**. It is written with square brackets `[]`, and every item is separated by a comma.

> **In plain words:** a list is a **backpack**. It holds many things in order, and each thing has a seat number just like the beads of a string. The big difference is that you can open the backpack and change what is inside (mutable), and the things don't all have to be the same kind.

## Heterogeneous data

A list is *heterogeneous*: one list can hold different data types side by side (strings, floats, ints, booleans, even other lists). You give every value separately, separated by commas.

```python
my_list = ['A', 'B', 'C', 0.123]
print(my_list)
print(type(my_list))

mixed = ['A string', 23, 100.232, 'o', True]
print(mixed)
print([type(x).__name__ for x in mixed])
print(len(my_list))
```

Output:

```text
['A', 'B', 'C', 0.123]
<class 'list'>
['A string', 23, 100.232, 'o', True]
['str', 'int', 'float', 'str', 'bool']
4
```

`len()` counts the items in the list. Note that `0.123` is one item, a float, and `'A string'` is one item, however long it is.

## Indexing, slicing, + and \*

These work exactly like strings: `list[start:stop:step]`, stop is excluded, negative indexes count from the end.

```python
l = ['one', 'two', 'three', 4, 5]
print(l[0], l[-1])
print(l[1:3])
print(l[0:5:3])
print(l[::-1])

print(l + ['new item', 5])
print(l)
l = l + ['x']
print(l)
print([1, 2] * 3)
```

Output:

```text
one 5
['two', 'three']
['one', 4]
[5, 4, 'three', 'two', 'one']
['one', 'two', 'three', 4, 5, 'new item', 5]
['one', 'two', 'three', 4, 5]
['one', 'two', 'three', 4, 5, 'x']
[1, 2, 1, 2, 1, 2]
```

`+` and `*` build a new list and do not change the original. Reassign (`l = l + [...]`) to keep the result.

## Mutability: the big difference from strings

```python
a = [1, 2, 3]
a[1] = 4
print(a)

s = 'abc'
try:
    s[1] = 'z'
except TypeError as e:
    print(e)
```

Output:

```text
[1, 4, 3]
'str' object does not support item assignment
```

A list item can be replaced in place. A string cannot.

## List methods

All of these change the list **in place** (the original list itself is modified), and most of them return `None`.

### append()

Adds **one** item to the end.

```python
a = [1, 4, 3]
a.append('append me!')
print(a)
a.append([6, 7])
print(a)
```

Output:

```text
[1, 4, 3, 'append me!']
[1, 4, 3, 'append me!', [6, 7]]
```

A list passed to `append` goes in as a single item (a list inside the list).

### extend()

Adds **each element** of an iterable to the end. This is the key difference from `append`.

> **In plain words:** `append` puts **one thing** into the backpack. If that thing is another bag, the whole bag goes in as one item. `extend` **tips out the other bag** and puts each of its things in separately.

```python
x = [1, 2, 3]
x.append([4, 5])
print(x)

x = [1, 2, 3]
x.extend([4, 5])
print(x)
```

Output:

```text
[1, 2, 3, [4, 5]]
[1, 2, 3, 4, 5]
```

### insert(index, object)

Places the object at the given index and pushes everything after it to the right.

```python
l = [1, 2, 3, 4, 5, 3]
l.insert(1, 'mango')
print(l)
```

Output:

```text
[1, 'mango', 2, 3, 4, 5, 3]
```

### pop()

Removes an item and gives it back. With no argument it removes the **last** item. With an index it removes that item.

> **In plain words:** `pop` takes something out of the backpack **and hands it to you**, so you can use it. With no number it takes the last thing, and with a number it takes the thing in that seat.

```python
b = [1, 2, 3, 4]
print(b.pop())
print(b)
print(b.pop(0))
print(b)

try:
    [1, 2][5]
except IndexError as e:
    print(e)
```

Output:

```text
4
[1, 2, 3]
1
[2, 3]
list index out of range
```

Indexing (or popping) a position that does not exist gives an `IndexError`.

### remove(value)

Removes the **first** item with that value (not by index). If the value is missing you get an error.

```python
l = [1, 2, 3, 4, 3]
l.remove(3)
print(l)

try:
    l.remove(99)
except ValueError as e:
    print(e)
```

Output:

```text
[1, 2, 4, 3]
list.remove(x): x not in list
```

`pop(i)` works by **position**, `remove(v)` works by **value**.

### count(value)

```python
l = [1, 2, 3, 2, 2]
print(l.count(2))
print(l.count(4))
```

Output:

```text
3
0
```

### index(value)

Returns the position of the first match. If the value is not in the list it raises an error (unlike string `find`, which gives `-1`).

```python
l = [1, 2, 3, 4, 5]
print(l.index(5))

try:
    l.index(12)
except ValueError as e:
    print(e)
```

Output:

```text
4
12 is not in list
```

### reverse()

Reverses the list in place (permanent).

```python
n = ['a', 'e', 'x', 'b', 'c', '1', '2']
n.reverse()
print(n)
```

Output:

```text
['2', '1', 'c', 'b', 'x', 'e', 'a']
```

### sort()

Sorts in place: alphabetical for strings, ascending for numbers. Use `reverse=True` for descending.

```python
n = ['2', '1', 'c', 'b', 'x', 'e', 'a']
n.sort()
print(n)
n.sort(reverse=True)
print(n)

nums = [1, 3, 47, 8, 12]
nums.sort()
print(nums)
print(nums.reverse())
print(nums)
```

Output:

```text
['1', '2', 'a', 'b', 'c', 'e', 'x']
['x', 'e', 'c', 'b', 'a', '2', '1']
[1, 3, 8, 12, 47]
None
[47, 12, 8, 3, 1]
```

Trap: `print(nums.reverse())` prints `None`, because the method changes the list and returns nothing. Never write `nums = nums.sort()`, as that makes `nums` equal to `None`.

### Quick reference

| Method | What it does | Returns |
| --- | --- | --- |
| `append(x)` | add one item at the end | `None` |
| `extend(iterable)` | add every element at the end | `None` |
| `insert(i, x)` | put `x` at index `i` | `None` |
| `pop(i=-1)` | remove by position | the removed item |
| `remove(x)` | remove first match by value | `None` |
| `count(x)` | how many times `x` appears | int |
| `index(x)` | position of first `x` | int (error if missing) |
| `reverse()` | reverse in place | `None` |
| `sort()` | sort in place | `None` |

# Day 2 – In my own words (what I understood)

- **Strings:** anything inside quotes is a string, and there is no data type *inside* it. `'0.5'` or `'445efddu43'` is still one string, because the quotes decide.
- A string is a **sequence**, so every character has a position (index) starting at **0**. `s[0]` is the first character and `s[-1]` is the last.
- **Slicing** takes a piece: `s[start:stop:step]`. The stop is not included. A negative step goes backwards, so `s[::-1]` reverses the string.
- Strings are **immutable**: I can't change a character inside one. What I can do is build a *new* string, with `+` (concatenation) or `*` (repetition), and reassign it to keep it.
- **Methods** are built-in actions I call with a dot and brackets: `upper()`, `lower()`, `split()`, `count()`, `find()`, `expandtabs()`, `endswith()`, `partition()` and the `is...` checks.
- `split` cuts at *every* match and drops it. `partition` cuts at the *first* match, keeps it, and gives three parts.
- **Lists:** like a string, but **mutable** and **heterogeneous**, so I can mix types: `['A', 'B', 'C', 0.123]`. Items are separated by commas.
- **List methods:** `append` (one item at the end), `extend` (each item of another list), `insert` (at a position), `pop` (remove by position and give it back), `remove` (remove by value), `count`, `index`, `sort` and `reverse` (both change the list itself).

# Day 2 – Extras from the notebook (not covered in class)

## Strings: quotes, printing and .format()

**Quotes inside a string.** If the text contains an apostrophe, wrap it in double quotes (or the other way round). Otherwise the apostrophe ends the string early and you get a `SyntaxError`.

```python
print("Now I'm ready to use the single quotes inside a string!")
```

Output:

```text
Now I'm ready to use the single quotes inside a string!
```

**Printing.** In Jupyter a bare string in a cell is displayed automatically, but only the **last** expression of a cell. Use `print()` to show several strings. `\n` inside a string starts a new line.

```python
print('Hello World 1')
print('Hello World 2')
print('Use \n to print a new line')
print('Line1\nLine2')
```

Output:

```text
Hello World 1
Hello World 2
Use 
 to print a new line
Line1
Line2
```

**`.format()`.** Puts values into the `{}` placeholders of a string. It does the same job as the f-string from Day 1.

```python
print('Insert another string with curly brackets: {}'.format('The inserted string'))
print('{} is {} years old'.format('Soni', 30))
print('{1} {0}'.format('world', 'hello'))
print('{name} likes {food}'.format(name='Soni', food='pizza'))
```

Output:

```text
Insert another string with curly brackets: The inserted string
Soni is 30 years old
hello world
Soni likes pizza
```

Empty `{}` fill in order, `{1}` and `{0}` pick by position, and `{name}` picks by keyword.

**`partition` and `endswith` on a real sentence.** The notebook ends with this sentence and the idea of checking its last character:

```python
s = 'i am joey from FRIENDS.I love pizza!'
print(s.partition('.'))
print(s.endswith('!'))
print(s[-1] == '!')
```

Output:

```text
('i am joey from FRIENDS', '.', 'I love pizza!')
True
True
```

`endswith('!')` is the same check as `s[-1] == '!'`.

# Lists: extras from the notebook

## Lists vs arrays in other languages

Python lists are more flexible than arrays in other languages for two reasons: they have **no fixed size** (you don't declare how big they will be) and **no fixed type** (the items can be of any type).

## Nested lists

A list can contain other lists. Use one index per level.

> **In plain words:** a backpack can hold a smaller bag, which can hold another bag. To reach something deep inside, you open one bag at a time, so you use one index per bag: `matrix[1][2][1]`.

```python
lst_1 = [1, 2, 3]
lst_2 = [4, 5, [9, 8]]
lst_3 = [7, 8, 9]
matrix = [lst_1, lst_2, lst_3]
print(matrix)
print(matrix[0][2])
print(matrix[1][2])
print(matrix[1][2][1])
```

Output:

```text
[[1, 2, 3], [4, 5, [9, 8]], [7, 8, 9]]
3
[9, 8]
8
```

`matrix[1]` is the second inner list, `[1][2]` is its third item (`[9, 8]`), and `[1][2][1]` is the second item of that (`8`).

## List comprehensions

A compact way to build a list from a `for` loop inside `[]`. (The instructor says this is fine to revisit later, once loops feel comfortable.)

> **In plain words:** a list comprehension is a **shortcut**: a loop and a list written in one line. Read it left to right, as "give me this, for each item, if it passes this test".

```python
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

# comprehension
print([row[1] for row in matrix])

# the same thing as a normal loop
first_col = []
for row in matrix:
    first_col.append(row[1])
print(first_col)

# with a condition
my_list = [1, 2, 3, 91, 4, 5, 6, 18, 9, 7]
print([i for i in my_list if i != 91 and i != 18])
```

Output:

```text
[2, 5, 8]
[2, 5, 8]
[1, 2, 3, 4, 5, 6, 9, 7]
```
