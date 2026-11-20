# Python Day 3

Nov 19, 2026 · @Soni Sindhal

## Day 3 – Tuples

### What a tuple is

A **tuple** is a container that holds several values, like a list, but it is **immutable**: once it is created, it cannot be modified. A tuple is written with **round brackets** (parentheses) `( )`, with the values separated by commas. A list uses square brackets `[ ]`.

> **In plain words:** a tuple is a **sealed box**. You pack the values in once, close the lid, and from then on you can look at what is inside but you can't add, remove or swap anything. A list is an open box.

```python
t = (1, 2, 3)
L = [1, 2, 3]
print(t, type(t))
print(L, type(L))
```

Output:

```text
(1, 2, 3) <class 'tuple'>
[1, 2, 3] <class 'list'>
```

The values in a tuple can be of different types, just like in a list:

```python
m = ('one', 2, 'one')
print(m)
print(len(m))
```

Output:

```text
('one', 2, 'one')
3
```

### Tuples allow duplicates

The same value can appear more than once in a tuple (as in a list). Each copy is its own item.

```python
d = (1, 1, 2, 3, 1)
print(d)
print(len(d))
```

Output:

```text
(1, 1, 2, 3, 1)
5
```

### Tuples, lists and strings keep their data in order

These three containers are all **sequences**: they store their items one after another, in the order you put them in, and every item has a position (index) starting at 0. That is why indexing and slicing work the same way on all three.

```python
s = 'hello'
l = [10, 20, 30]
tt = (10, 20, 30)
print(s[1], l[1], tt[1])
print(s[::-1], l[::-1], tt[::-1])
```

Output:

```text
e 20 20
olleh [30, 20, 10] (30, 20, 10)
```

> **In plain words:** "in order" does **not** mean sorted. It means the container remembers *where* each item was placed. The item you put in seat 1 stays in seat 1.

|  | String | List | Tuple |
| --- | --- | --- | --- |
| Brackets | quotes `' '` | `[ ]` | `( )` |
| Can it be changed (mutable)? | No | Yes | No |
| Allows duplicates? | Yes | Yes | Yes |
| Keeps order, has indexes? | Yes | Yes | Yes |

### Indexing and slicing in tuples

A tuple is a sequence, so indexing and slicing work **exactly as they do for lists and strings**. Index positions start at 0, negative indexes count from the end, and in a slice `[start:stop:step]` the stop is not included.

```python
t = ('a', 'b', 'c', 'd', 'e')
print(t[0], t[2])
print(t[-1], t[-2])
print(t[1:4])
print(t[:2])
print(t[2:])
print(t[::2])
print(t[::-1])
```

Output:

```text
a c
e d
('b', 'c', 'd')
('a', 'b')
('c', 'd', 'e')
('a', 'c', 'e')
('e', 'd', 'c', 'b', 'a')
```

- Indexing with one number gives you **one item** (`t[0]` is `'a'`).
- Slicing gives you a **new tuple** (`t[1:4]` is `('b', 'c', 'd')`), and the original tuple is untouched.
- An index that doesn't exist raises an error:

```python
try:
    print(t[5])
except IndexError as e:
    print(e)
```

Output:

```text
tuple index out of range
```

> **In plain words:** the items sit in numbered seats starting at 0. A single number asks "who is in this seat?". A slice like `[1:4]` asks "give me seats 1 to 3" (it stops *before* 4) and hands you a new small tuple.

### Tuple methods: only two

A list has many methods (`append`, `sort`, `remove` and more), but a tuple has only **two**: `.index()` and `.count()`. The rest of the list methods would change the data, and a tuple can't be changed. Both of these only *look* at the tuple.

```python
m = ('one', 2, 'one')
print(m.index(2))
print(m.index('one'))
print(m.count('one'))
print(m.count('zzz'))
```

Output:

```text
1
0
2
0
```

- `.index(value)` returns the **position** of the first match. For `'one'` that is 0, even though it appears again at position 2.
- `.count(value)` returns **how many times** the value appears. If it isn't there, you get `0`.
- `.index()` on a value that is missing gives an error (`ValueError`), unlike `.count()`:

```python
try:
    m.index('zzz')
except ValueError as e:
    print(e)
```

Output:

```text
tuple.index(x): x not in tuple
```

> **In plain words:** `.index()` answers "where is it?" and `.count()` answers "how many are there?". Neither one changes the tuple, so they are the only two buttons a sealed box needs.

### Immutability: what happens if you try to change one

```python
t = (1, 2, 3)
try:
    t[0] = 'change'
except TypeError as e:
    print(e)

try:
    t.append(4)
except AttributeError as e:
    print(e)
```

Output:

```text
'tuple' object does not support item assignment
'tuple' object has no attribute 'append'
```

The first error is the same one you get when you try to change a letter of a string. The second tells you tuples don't have an `append` at all, because a tuple can't grow.

### Changing a tuple: convert to a list, change it, convert back

You can't edit a tuple, but you can get around it in three steps:

1. Convert the tuple to a list with `list()`.
2. Make your change on the list.
3. Convert the list back to a tuple with `tuple()`.

```python
x = (1, 2, 3)
print(type(x))

temp_list = list(x)      # step 1: tuple -> list
print(type(temp_list))
temp_list.append(4)      # step 2: change the list
temp_list[0] = 'changed'
print(temp_list)

x = tuple(temp_list)     # step 3: list -> tuple
print(type(x))
print(x)
```

Output:

```text
<class 'tuple'>
<class 'list'>
['changed', 2, 3, 4]
<class 'tuple'>
('changed', 2, 3, 4)
```

> **In plain words:** you don't open the sealed box. You copy everything into an open box (a list), make your changes there, and then seal it again in a **new** box (a new tuple). The original tuple was never changed. The name `x` just points to the new one.

This is the same idea as reassigning a plain variable, which does not "edit" the old value either:

```python
a = 1
a = 2
print(a)
```

Output:

```text
2
```

### When to use a tuple

Tuples are used less often than lists, but they are the right choice when the data **must not change**, such as the days of the week or the dates on a calendar. If you pass an object around a program and need to be sure nobody changes it by accident, a tuple gives you that safety (called *data integrity*).&#32;

## Day 3 – Sets

### What a set is

A **set** is an **unordered** collection of **unique** values. Unlike lists, tuples and strings, a set does **not** keep its data in a sequence, and it never holds duplicates. A set is written with curly brackets `{ }`.

> **In plain words:** a set is a **bag of marbles**. You can throw marbles in and look inside, but the marbles have no seat numbers and no order. And the bag never keeps two identical marbles: if you add one that is already there, nothing changes.

```python
s = {"banana", "apple", "cherry", "orange"}
print(len(s))
print(type(s))
print('apple' in s)
```

Output:

```text
4
<class 'set'>
True
```

If you print a set of text values, the order can come out differently each time you run the program. That is normal for a set, because order is not part of what a set stores.

### Stored in hash memory

When a value goes into a set, Python does not place it in the next free seat. It runs the value through a **hash function**, which turns the value into a number, and that number decides *where* in memory the value is stored. This kind of storage is called a **hash table** (hash memory). It is the reason a set is fast at checking "is this value in here?", and also the reason it has no order and no duplicates: the same value always gets the same spot.

> **In plain words:** think of a library where the book's title decides which shelf it goes on, instead of putting books in the next free space. To find a book you go straight to its shelf, so there is no searching. But the books are not in any "first, second, third" order, and the same title can only ever be on one shelf.

### Unique values only

```python
d = {1, 2, 2, 3, 3, 3}
print(d)

x = set()
x.add(3)
x.add(2)
x.add(1)
print(x)
x.add(1)
x.add(1)
print(x, len(x))
```

Output:

```text
{1, 2, 3}
{1, 2, 3}
{1, 2, 3} 3
```

The repeated values were dropped. Adding `1` again changes nothing, and no error is raised.

To make an **empty** set you must write `set()`. A plain `{}` makes an empty *dictionary* (the next topic), not a set.

```python
print(type(set()))
print(type({}))
```

Output:

```text
<class 'set'>
<class 'dict'>
```

### Adding data: add()

`add()` puts one value into the set. If the value is already there, nothing happens.

```python
x = set()
x.add(3)
x.add(2)
x.add(1)
print(x)
```

Output:

```text
{1, 2, 3}
```

### No indexing and no slicing

Since a set has no order, its items have no positions, so there is nothing to index or slice. Trying it raises an error:

```python
x = {1, 2, 3}
try:
    x[1]
except TypeError as e:
    print(e)

try:
    x[0:2]
except TypeError as e:
    print(e)
```

Output:

```text
'set' object is not subscriptable
'set' object is not subscriptable
```

"Not subscriptable" means you can't use `[ ]` on it. To use the values you loop over the set or check membership with `in`.

### remove() and discard()

Both delete a value from the set. The difference is what happens when the value **isn't there**:

- `remove(value)` raises an error (`KeyError`).
- `discard(value)` stays silent and does nothing.

```python
r = {1, 2, 3, 5}
r.remove(5)
print(r)

try:
    r.remove(99)
except KeyError as e:
    print('KeyError:', e)

r.discard(99)
print(r)
r.discard(3)
print(r)
```

Output:

```text
{1, 2, 3}
KeyError: 99
{1, 2, 3}
{1, 2}
```

`discard(99)` didn't complain even though 99 wasn't in the set, while `discard(3)` removed the 3. That is why `discard` is the safe choice when you aren't sure the value is there.

### clear()

Removes **everything** from the set and leaves an empty set.

```python
c = {1, 2, 3}
c.clear()
print(c)
print(len(c))
```

Output:

```text
set()
0
```

### pop()

Removes **one value** from the set and gives it back to you. You don't choose which one: a set has no order, so Python removes an arbitrary item (it looks random). That means you can't predict which value comes out.

```python
p = {10, 20, 30, 40}
v = p.pop()
print(v in {10, 20, 30, 40})
print(v not in p)
print(len(p))
```

Output:

```text
True
True
3
```

Whatever value `pop()` returned was one of the four, it is no longer in the set, and the set now has three values left. (Unlike `list.pop()`, you can't give it a position, because a set has no positions.)

### Quick reference

| Method | What it does | If the value is missing |
| --- | --- | --- |
| `add(x)` | add one value | n/a (adding a duplicate does nothing) |
| `remove(x)` | delete `x` | error (`KeyError`) |
| `discard(x)` | delete `x` | no error |
| `pop()` | remove and return some value | error on an empty set |
| `clear()` | delete everything | n/a |

### Getting unique values from a list

Because a set drops duplicates, converting a list to a set is the quickest way to get its unique values:

```python
l = [1, 1, 2, 2, 3, 4, 5, 6, 1, 1]
print(set(l))
print(list(set(l)))
```

Output:

```text
{1, 2, 3, 4, 5, 6}
[1, 2, 3, 4, 5, 6]
```

## Day 3 – Dictionaries

### What a dictionary is

A **dictionary** also uses a hash table, like a set, but instead of storing single values it stores **pairs**: a **key** and the **value** that goes with it. You write it in curly brackets as `key : value` pairs separated by commas. To get a value out, you **call its key**.

> **In plain words:** a dictionary is a **real dictionary** (or a phone book). You don't look up "the 5th entry", you look up the *word* (the key) and it gives you its *meaning* (the value). Names go in as keys, and what they stand for comes out as values.

```python
d = {'key1': 'value1', 'key2': 'value2'}
print(d)
print(type(d))
print(d['key1'])
```

Output:

```text
{'key1': 'value1', 'key2': 'value2'}
<class 'dict'>
value1
```

Sets and dictionaries are not sequences. A dictionary is a **mapping**: its items are found by **key**, not by position. So `d[0]` does not mean "the first item", it means "the value whose key is 0". Asking for a key that doesn't exist raises a `KeyError`:

```python
try:
    d['nokey']
except KeyError as e:
    print('KeyError:', e)

try:
    d[0]
except KeyError as e:
    print('KeyError:', e)
```

Output:

```text
KeyError: 'nokey'
KeyError: 0
```

### Values can be any type, and values can repeat

The values can be of **any data type**: numbers, strings, lists, even other dictionaries. The same value may be used under different keys, so duplication is allowed in the **values**.

```python
dup = {'key1': 2, 'key5': 2}
print(dup)
print(dup['key1'] == dup['key5'])
```

Output:

```text
{'key1': 2, 'key5': 2}
True
```

Keys are different: a key must be **unique**. If you write the same key twice, the later value replaces the earlier one and only one entry is kept.

```python
k = {'key1': 'first', 'key1': 'second'}
print(k)
print(len(k))
```

Output:

```text
{'key1': 'second'}
1
```

> **In plain words:** many different words in a dictionary can have the same meaning (duplicate values), but you can't have the same word listed twice (duplicate keys). If you try, the new meaning overwrites the old one.

A key also has to be an immutable type, such as a string, number, boolean or tuple. A list can't be a key.

### Different types as values, and using methods on a value

```python
my_dict = {'key1': 123, 'key2': [12, 23, 33], 'key3': ['item0', 'item1', 'item2']}
print(my_dict['key1'])
print(my_dict['key2'])
print(my_dict['key3'][1])
print(my_dict['key3'][0].upper())
```

Output:

```text
123
[12, 23, 33]
item1
ITEM0
```

`my_dict['key3']` gives back the list, so you can keep going: `[1]` indexes that list, and `[0].upper()` takes its first item and calls a string method on it. A value behaves exactly like the thing it is.

### Changing values, and +=, -=

You can change the value of a key by assigning to it. The arithmetic operators work on the values, including `-`, `+=` and `-=`:

```python
my_dict = {'key1': 123}
my_dict['key1'] = my_dict['key1'] - 100
print(my_dict['key1'])
my_dict['key1'] -= 20
print(my_dict['key1'])
my_dict['key1'] += 50
print(my_dict['key1'])
```

Output:

```text
23
3
53
```

`my_dict['key1'] -= 20` is shorthand for `my_dict['key1'] = my_dict['key1'] - 20`.

**Creating keys by assignment.** Start with an empty dictionary `{}` and add to it. Assigning to a key that doesn't exist creates it. Assigning to one that does exist overwrites it.

```python
e = {}
print(type(e))
e['animal'] = 'joey'
print(e)
e['answer'] = 42
print(e)
e['answer'] = 43
print(e)
```

Output:

```text
<class 'dict'>
{'animal': 'joey'}
{'animal': 'joey', 'answer': 42}
{'animal': 'joey', 'answer': 43}
```

### Nested dictionaries

A dictionary can hold another dictionary as a value, which can hold another, and so on. To reach the inside, call one key after another.

```python
n = {'key1': {'nestkey': {'subnestkey': 123}}}
print(n['key1'])
print(n['key1']['nestkey'])
print(n['key1']['nestkey']['subnestkey'])
```

Output:

```text
{'nestkey': {'subnestkey': 123}}
{'subnestkey': 123}
123
```

> **In plain words:** a nested dictionary is a **cupboard of boxes inside boxes**. Each key opens one box, and inside you find another box. You keep opening until you reach the value you want.

### Example: counting characters (string compression)

The notebook has this example with `x = 'aabcba'`. The goal is to **count how many times each character appears**, and then turn those counts into a short string. It works in two steps.

**Step 1: count each character in a dictionary.** The characters are the keys and their counts are the values. For every character `i` in the string: if it is already a key in the dictionary, add 1 to its count. If not, this is the first time we've seen it, so add it with the count 1.

```python
x = 'aabcba'
d = {}
for i in x:
    if i in d:
        d[i] += 1
    else:
        d[i] = 1
print(d)
```

Output:

```text
{'a': 3, 'b': 2, 'c': 1}
```

Walking through it: `a` (new, 1), `a` (seen, 2), `b` (new, 1), `c` (new, 1), `b` (seen, 2), `a` (seen, 3).

**Step 2: join each character with its count into one string.** `d.items()` gives each key and value together, and an f-string joins them:

```python
c = ''
for i, v in d.items():
    c += f'{i}{v}'
print(c)
```

Output:

```text
a3b2c1
```

So `'aabcba'` becomes `'a3b2c1'`: three a's, two b's, one c.

Note: the comment in the notebook says `a3b3c1`, but the correct answer is `a3b2c1`, because there are only two `b`s. The second comment in the notebook, `a2b1c1b1a1`, is a *different* kind of compression: it counts **runs of the same letter next to each other** (aa, b, c, b, a), so the order is kept.

### Shallow copy and deep copy

This matters when you copy something that has **a container inside a container**, like a list of lists.

- A **shallow copy** makes a new outer container, but the inner containers are **shared** with the original. Change something inside an inner list, and you change it in both the original and the copy.
- A **deep copy** copies everything, all the way down. The copy is completely independent, so changing it does not touch the original.

> **In plain words:** imagine a folder that holds two sheets of paper. A shallow copy gives you a **new folder holding the same two sheets**: if you scribble on a sheet, both folders show it. A deep copy gives you a new folder with **photocopies of the sheets**: scribbling on your copy leaves the original clean.

**Shallow copy.** With `copy.copy()`:

```python
import copy

original = [[1, 2], [3, 4]]
shallow = copy.copy(original)
print(shallow == original)
print(shallow is original)
print(shallow[0] is original[0])

shallow[0][0] = 12
print('original', original)
print('shallow', shallow)
```

Output:

```text
True
False
True
original [[12, 2], [3, 4]]
shallow [[12, 2], [3, 4]]
```

`shallow is original` is `False`, so the outer lists are different. But `shallow[0] is original[0]` is `True`: the inner list is the **same object** in both. That is why changing `shallow[0][0]` changed both.

Only changes *inside* the shared inner lists show up in both. A change to the outer list itself, such as adding a new item, affects only the copy:

```python
shallow.append([5, 6])
print('original', original)
print('shallow', shallow)
```

Output:

```text
original [[12, 2], [3, 4]]
shallow [[12, 2], [3, 4], [5, 6]]
```

**Deep copy.** With `copy.deepcopy()`:

```python
import copy

original = [[1, 2], [3, 4]]
deep = copy.deepcopy(original)

deep[0][0] = 12
print('original', original)
print('deep', deep)
```

Output:

```text
original [[1, 2], [3, 4]]
deep [[12, 2], [3, 4]]
```

The original is unchanged and only the deep copy was updated.

**A trap in the notebook example.** The notebook's first example writes `shallow = original` (the `copy.copy(...)` line is commented out). That is not a copy at all. It just gives the **same list a second name**, so *any* change shows up under both names:

```python
original = [[1, 2], [3, 4]]
shallow = original
shallow[0][0] = 12
print(original)
print(shallow)
print(shallow is original)
```

Output:

```text
[[12, 2], [3, 4]]
[[12, 2], [3, 4]]
True
```

The printed result looks the same as a real shallow copy, but the reason is different. Use `copy.copy()` when you want an actual shallow copy.

### Dictionary methods: keys(), values(), items()

These three let you look at the **parts** of a dictionary.

```python
d = {'key1': 1, 'key2': 2, 'key3': 3}
print(d.keys())
print(d.values())
print(d.items())
```

Output:

```text
dict_keys(['key1', 'key2', 'key3'])
dict_values([1, 2, 3])
dict_items([('key1', 1), ('key2', 2), ('key3', 3)])
```

- `.keys()` gives all the **keys**.
- `.values()` gives all the **values**.
- `.items()` gives every **key and value together**, each pair as a tuple.

They return special "view" objects, not plain lists. Wrap them in `list()` if you want a normal list:

```python
print(list(d.keys()))
print(list(d.values()))
print(list(d.items()))
```

Output:

```text
['key1', 'key2', 'key3']
[1, 2, 3]
[('key1', 1), ('key2', 2), ('key3', 3)]
```

`.items()` is most useful in a `for` loop, because you can take the key and the value in one go (this is what the character-counting example used):

```python
for key, val in d.items():
    print(key, val)
```

Output:

```text
key1 1
key2 2
key3 3
```

> **In plain words:** `.keys()` is the list of **words** in the dictionary, `.values()` is the list of **meanings**, and `.items()` is every **word with its meaning** side by side.

## Day 3 – Functions

### What a function is

A **function** is a group of statements bundled together under a name, so you can run them **whenever you want, as many times as you want**, instead of writing the same code again and again. A function can also take **inputs** (called *parameters*), so the same code can work on different values.

> **In plain words:** a function is a **recipe with a name**. You write the steps once and give the recipe a name. Every time you want the dish, you just say the name. The ingredients you hand over (the inputs) can be different each time.

You have already used functions that Python provides: `print()`, `len()`, `type()`. Now you create your own.

### def: defining a function

The keyword **`def`** (short for *define*) creates a function. The pattern is:

```python
def name_of_function(parameter1, parameter2):
    # the code that runs when the function is called (indented)
    return result
```

- `def`, then a space, then the **name** of the function.
- The inputs go in **round brackets**, separated by commas. These are the *parameters*.
- A **colon `:`** at the end of the line.
- The code of the function goes on the next lines, **indented**. Python uses the indentation to know what belongs to the function.
- Optionally, a *docstring* (a short description in triple quotes) goes first inside the function.

You wrote it as `def sum = a, b`. The correct form uses brackets and a colon, not an equals sign: `def add(a, b):`. Also, avoid naming a function `sum`, because `sum` is already a built-in Python function (the same naming rule from Day 1), so `add` is a safer name.

Defining a function does **not** run it. Nothing happens until you **call** it by writing its name with brackets.

```python
def say_hello():
    print('hello')

say_hello()
say_hello()
```

Output:

```text
hello
hello
```

The function was defined once and called twice.

**Parameters and arguments.** A function can take inputs. The names in the definition (`name`) are *parameters*. The actual values you pass when calling it (`'Kota'`) are *arguments*.

```python
def greeting(name):
    print(f'Hello {name}!')

greeting('Kota')
greeting(90)
```

Output:

```text
Hello Kota!
Hello 90!
```

### print vs return

A function can give something back in two different ways, and they are not the same:

- **`print`** only **shows** the value on the screen. The value is not handed back to the program, so you can't store it or use it afterwards.
- **`return`** **sends the value back** to whoever called the function, so you can save it in a variable and **reuse** it.

> **In plain words:** `print` is **saying the answer out loud**. Anyone in the room hears it, but nobody has it written down. `return` is **handing over the answer on a piece of paper**. You can keep it, add to it, or give it to someone else.

Here are two functions that do the same sum, one with `print` and one with `return`:

```python
def add_print(a, b):
    print(a + b)

def add_return(a, b):
    return a + b

r1 = add_print(5, 6)     # prints 11 on the screen
r2 = add_return(5, 6)    # nothing printed, the 11 is stored in r2
print('r1 =', r1)
print('r2 =', r2)
```

Output:

```text
11
r1 = None
r2 = 11
```

The first line, `11`, came from the `print` inside `add_print`. Then `r1` is **`None`**, which means "nothing": the function showed the value but never handed it back. `r2` really holds `11`.

So you can keep calculating with `r2`, but not with `r1`:

```python
try:
    print(r1 + 9)
except TypeError as e:
    print(e)

print(r2 + 9)
```

Output:

```text
unsupported operand type(s) for +: 'NoneType' and 'int'
20
```

The same thing happens in the earlier `greeting` function: it only prints, so `x = greeting(90)` leaves `x` as `None`.

```python
x = greeting(90)
print(x)
```

Output:

```text
Hello 90!
None
```

**When to use which.** Use `return` when you need the result later, which is most of the time. Use `print` when the only goal is to show something on the screen.

One more thing about `return`: it **ends the function immediately**. Any code after it in the function does not run.

```python
def early():
    return 'first'
    print('never runs')

print(early())
```

Output:

```text
first
```

### Polymorphism: the same function, different types

A function does not fix what type its inputs must be. The **same function** can work on different types of data, and the result depends on what you give it. This is called **polymorphism** ("many forms").

```python
def add(a, b):
    return a + b

print(add(5, 6))
print(add('df', 'pf'))
print(add([1, 2], [3]))
print(add(2.5, 1))
```

Output:

```text
11
dfpf
[1, 2, 3]
3.5
```

- Two integers: `+` **adds** them (`11`).
- Two strings: `+` **joins** them (`dfpf`).
- Two lists: `+` joins them into one list.
- A float and an integer: gives a float.

The function didn't change at all. What changed was the arguments, and `+` behaves according to the type it is given.

> **In plain words:** think of a **"combine" button**. Give it two numbers and it adds them. Give it two words and it sticks them together. You pressed the same button, and each kind of thing got combined in its own way.

The types still have to make sense together. Mixing a string and a number fails:

```python
try:
    add('a', 1)
except TypeError as e:
    print(e)
```

Output:

```text
can only concatenate str (not "int") to str
```

This works because Python doesn't make you declare types (dynamic typing, from Day 1).

### Example: prime numbers

A **prime number** is a number greater than 1 that can be divided evenly **only by 1 and by itself**. For example 7 is prime (nothing but 1 and 7 divide it), and 8 is not prime (2 and 4 also divide it). The number 1 is **not** considered prime.

> **In plain words:** a prime number can't be shared out into equal smaller groups. 7 sweets can only be split into 7 groups of one, or one group of seven. 8 sweets can also be split into 2 groups of four.

The idea of the function: take a number, and test whether any number from 2 up to just below it divides it with **no remainder** (`%` gives the remainder, so `num % n == 0` means "divides evenly"). If one does, it isn't prime.

```python
def is_prime(num):
    for n in range(2, num):
        if num % n == 0:
            print('not prime')
            break
    else:
        print('prime')

is_prime(7)
is_prime(8)
```

Output:

```text
prime
not prime
```

How it works:

- `range(2, num)` tries every number from 2 up to `num - 1`.
- `num % n == 0` asks "does `n` divide `num` evenly?". If yes, it prints `not prime` and `break` stops the loop at once, because one divisor is enough.
- The `else` belongs to the **`for`**, not the `if`. It runs only if the loop finished **without** hitting `break`, so no divisor was found and the number is prime.
- Walk through `is_prime(8)`: `n = 2` gives `8 % 2 == 0`, so it prints `not prime` and stops.
- Walk through `is_prime(7)`: it tries 2, 3, 4, 5 and 6, none divides 7, so the loop ends normally and the `else` prints `prime`.

**A flaw to know about.** This version says `1` is prime, which is wrong, because `range(2, 1)` is empty so the loop never runs and the `else` fires:

```python
is_prime(1)
```

Output:

```text
prime
```

**A better version using `return`.** It checks for numbers below 2 first, and it returns `True` or `False` instead of printing, so you can reuse the answer (for example, to build a list of primes):

```python
def is_prime2(num):
    if num < 2:
        return False
    for n in range(2, num):
        if num % n == 0:
            return False
    return True

print(is_prime2(7))
print(is_prime2(10))
print(is_prime2(1))
print([n for n in range(1, 21) if is_prime2(n)])
```

Output:

```text
True
False
False
[2, 3, 5, 7, 11, 13, 17, 19]
```

This ties the topics together: `return` lets another part of the program (the list at the end) *use* the answer, which a `print` version could not do.

## Day 3 – Iterators and Generators

### What they are, and how a for loop really works

To **iterate** means to go through the items of something one at a time, which is what a `for` loop does. Two ideas sit behind every `for` loop:

- An **iterable** is anything you can loop over: a string, list, tuple, set, dictionary.
- An **iterator** is the object that actually hands you the items **one at a time** and remembers where it is. Any object that has `__iter__()` and `__next__()` is an iterator.

A `for` loop is really doing this behind the scenes: it calls `iter()` on your iterable to get an iterator, then calls `next()` again and again to get each item, and stops when the items run out. A **generator** is a special, easy way of writing your own iterator.

> **In plain words:** an iterable is a **box of sweets**. An iterator is a **person holding the box who gives you one sweet each time you say "next"**, and who remembers which sweet comes after this one. When the box is empty, they say "no more". A `for` loop is you saying "next" over and over until they say "no more".

A note on what you mentioned: you will rarely write `iter()` and `next()` by hand in real projects, because a `for` loop does it for you. But the ideas behind them are used everywhere, and **generators are widely used in production**, especially for big data (see the memory example below).

### iter() and next()

- `iter(x)` turns an iterable into an **iterator**.
- `next(it)` gives the **next item** from the iterator.
- When there are no more items, `next()` raises a **`StopIteration`** error. This is the signal "nothing left". A `for` loop catches this error quietly and stops.

A string is **iterable** (you can loop over it), but it is **not an iterator** yet, so `next()` does not work on it directly:

```python
l = 'joey'
try:
    next(l)
except TypeError as e:
    print(e)
```

Output:

```text
'str' object is not an iterator
```

`iter()` turns it into one:

```python
s = iter(l)
print(next(s))
print(next(s))
print(next(s))
print(next(s))
try:
    next(s)
except StopIteration:
    print('StopIteration')
```

Output:

```text
j
o
e
y
StopIteration
```

The fifth `next()` raised `StopIteration` because all four letters had been given out. The same works for a list:

```python
nums = [1, 2, 3]
it = iter(nums)
print(next(it))
print(next(it))
print(next(it))
```

Output:

```text
1
2
3
```

**A for loop written by hand** with `iter` and `next`. This is how a loop is created from these two functions:

```python
it = iter([10, 20, 30])
while True:
    try:
        item = next(it)
    except StopIteration:
        break
    print(item)
```

Output:

```text
10
20
30
```

This does exactly what `for item in [10, 20, 30]: print(item)` does. The `for` version is just a shorter way to write it.

### Generators and yield

A **generator** is a special type of iterator that you write **like a function**, but with the keyword **`yield`** instead of `return`.

Compare a normal function that prints cubes with a generator that **yields** them:

```python
def gencube_print(n):
    for i in range(n):
        print(i**3)

def gencubes(n):
    for num in range(n):
        yield num**3
```

Calling the first one runs the loop straight away and prints everything. Calling the second one does **not** run it. It gives you a **generator object**, which is like a ready-to-go machine that hasn't started yet:

```python
g = gencubes(5)
print(type(g))
print(g)
```

Output:

```text
<class 'generator'>
<generator object gencubes at 0x7f1a6a3ea9b0>
```

(The `0x...` memory address will be different on your computer.) That is what you see when you run `gencubes(5)` on its own: no cubes yet, just the generator object. The `5` is the `n` you passed, so it is ready to produce the cubes of 0 to 4, one at a time, when asked.

You ask it for values with `next()` or with a `for` loop:

```python
print(next(g))
print(next(g))
print(next(g))
for x in g:
    print('loop', x)
```

Output:

```text
0
1
8
loop 27
loop 64
```

The three `next()` calls gave `0`, `1` and `8`. The `for` loop then **carried on from where it left off** and gave `27` and `64`. It did not start again from 0.

**yield pauses and resumes.** Each time the generator reaches `yield`, it hands over a value and **pauses**, remembering exactly where it was, including the values of its variables. The next `next()` **resumes right after the `yield`**. This is the key difference from `return`.

```python
def counter():
    print('start')
    yield 1
    print('middle')
    yield 2
    print('end')

c = counter()
print('created')
print(next(c))
print(next(c))
try:
    next(c)
except StopIteration:
    print('finished')
```

Output:

```text
created
start
1
middle
2
end
finished
```

Nothing ran when `counter()` was called (only `created` printed). The `start` appeared on the first `next()`, the function paused at `yield 1`, then resumed to print `middle`, paused at `yield 2`, and on the third `next()` it printed `end` and ran out of code, which raises `StopIteration`.

> **In plain words:** a generator is a **vending machine that makes one item each time you press the button**. It does not cook all the food at once. It makes one thing, hands it over, and waits. Press the button again and it carries on with the next one.

**A generator is used up once you have gone through it.** When it is finished, looping over it again gives nothing:

```python
g = gencubes(3)
print(list(g))
print(list(g))
```

Output:

```text
[0, 1, 8]
[]
```

To go through the values again, call `gencubes(3)` again to get a fresh generator.

### return vs yield

|  | `return` | `yield` |
| --- | --- | --- |
| What it does | Sends back a value and **ends** the function | Sends back a value and **pauses** the function |
| Can it give several values? | No, the function stops at the first `return` | Yes, one value each time you ask |
| What you get when you call the function | The result straight away | A generator object, values come when you ask |
| Remembers where it was? | No, it starts from the top on the next call | Yes, it resumes after the last `yield` |

```python
def f():
    return 1
    return 2

def gg():
    yield 1
    yield 2

print(f())
print(list(gg()))
```

Output:

```text
1
[1, 2]
```

`f()` stops at the first `return`, so `2` is never reached. `gg()` gives both values.

### Example: Fibonacci numbers

The Fibonacci sequence starts `1, 1` and each next number is the **sum of the previous two**: 1, 1, 2, 3, 5, 8... The notebook writes it as a generator:

```python
def genfibon(n):
    a = 1
    b = 1
    for i in range(n):
        yield a
        a, b = b, a + b

print(list(genfibon(10)))
```

Output:

```text
[1, 1, 2, 3, 5, 8, 13, 21, 34, 55]
```

`a, b = b, a + b` updates both numbers at once: `a` becomes the old `b`, and `b` becomes the old `a + b`. Because the function pauses at `yield a`, it only needs to remember the **last two numbers**, not the whole list.

The same thing as a normal function has to collect **every** result in a list and return it at the end:

```python
def fibon(n):
    a = 1
    b = 1
    output = []
    for i in range(n):
        output.append(a)
        a, b = b, a + b
    return output

print(fibon(10))
```

Output:

```text
[1, 1, 2, 3, 5, 8, 13, 21, 34, 55]
```

### Why use generators: saving memory

A list holds **all** its values in memory at once. A generator holds only the **one value it is working on**, which matters a lot when the data is huge (millions of rows, a large file). Compare a list and a generator of the same one million squares:

```python
import sys

big_list = [i * i for i in range(1000000)]
big_gen = (i * i for i in range(1000000))
print(sys.getsizeof(big_list))
print(sys.getsizeof(big_gen))
print(sum(big_gen))
```

Output:

```text
8448728
200
333332833333500000
```

The list takes roughly 8 million bytes (about 8 MB) just for the list, while the generator takes about 200 bytes and still produces every value when `sum()` asks for them. (The exact sizes differ a little between Python versions.) The round brackets `( )` with a `for` inside make a *generator expression*, a short way to write a generator.

> **In plain words:** a list is **printing a whole book before you read it**. A generator is **reading it one page at a time**. For a huge book you don't need all the pages in your hands at once.

For data engineering this matters: generators let you process very large files or streams of data one row at a time without loading everything into memory.

## Day 3 – map()

### What map does

`map()` applies a function to **every item** of an iterable (a list, tuple, string...) and gives you the results. It takes **two arguments**:

1. a **function**
2. an **iterable** (the data to run the function on)

```python
map(function, iterable)
```

The point of `map` is to **avoid writing the same loop again and again**. You define the function once at the top, and then `map` pulls that function over all the data for you, so you don't write a `for` loop each time.

> **In plain words:** think of a **photocopier with a stamp**. The function is the stamp. You put a whole stack of papers (the list) into the machine, and `map` stamps every single sheet and hands you back the stamped stack. You didn't stamp each page yourself.

### Example: Celsius and Fahrenheit

First define the two conversion functions once:

```python
def celsius(T):
    return (5/9) * (T - 32)

def fahrenheit(T):
    return (9/5) * T + 32

temp = [0, 22.5, 40, 100]
```

**Without `map`**, you write a loop and collect the answers yourself:

```python
out = []
for t in temp:
    out.append(celsius(t))
print(out)
```

Output:

```text
[-17.77777777777778, -5.277777777777778, 4.444444444444445, 37.77777777777778]
```

**With `map`**, it is one line. This is what you described, `list(map(celsius, temp))`:

```python
c_temps = list(map(celsius, temp))
print(c_temps)
```

Output:

```text
[-17.77777777777778, -5.277777777777778, 4.444444444444445, 37.77777777777778]
```

The result is the same, but you didn't write the loop. You can use the other function to convert back, with the same one line:

```python
print(list(map(fahrenheit, c_temps)))
```

Output:

```text
[0.0, 22.5, 40.0, 100.0]
```

We got our original temperatures back.

Notice that in `map(celsius, temp)` you write the function name **without brackets**. You are handing over the function itself so `map` can use it on each item. If you wrote `celsius(temp)`, you would be *calling* it right now.

### Why the list() around it?

In Python 3, `map()` does **not** give you a list. It gives you a **map object**, which is an **iterator** (the same idea you just learned). Nothing is calculated until you ask for the values:

```python
m = map(celsius, temp)
print(type(m))
print(m)
```

Output:

```text
<class 'map'>
<map object at 0x7f48a31b0190>
```

(The `0x...` address will be different on your computer.) You can pull values out with `next()`, a `for` loop, or turn the whole thing into a list with `list()`:

```python
m = map(celsius, temp)
print(next(m))
print(next(m))
print(list(m))
print(list(m))
```

Output:

```text
-17.77777777777778
-5.277777777777778
[4.444444444444445, 37.77777777777778]
[]
```

The first two values came out with `next()`. `list(m)` then collected the **remaining two**. After that the map object is used up, so the last `list(m)` is empty. (The notebook text says `map` returns a list. That was true in old Python 2, but in Python 3 it returns this iterator, so we wrap it in `list()`.)

### map works with any function

Built-in functions work too, not only your own:

```python
def cube(x):
    return x ** 3

print(list(map(cube, [1, 2, 3, 4, 5, 6])))
print(list(map(len, ['ruchi', 'Nikhil', 'phoebee', 'swapna'])))
print(list(map(int, ['1', '2', '3'])))
```

Output:

```text
[1, 8, 27, 64, 125, 216]
[5, 6, 7, 6]
[1, 2, 3]
```

- `cube` was applied to each number.
- `len` gave the length of each word.
- `int` converted each text number to a real integer.

### map with more than one iterable

If the function takes more than one parameter, give `map` **one iterable per parameter**. `map` takes the first item of each, then the second item of each, and so on.

```python
def add3(x, y, z):
    return x + y + z

a = [1, 2, 3, 4]
b = [5, 6, 7, 8]
c = [9, 10, 11, 12, 4, 5]
print(list(map(add3, a, b, c)))
```

Output:

```text
[15, 18, 21, 24]
```

The first result is `1 + 5 + 9 = 15`, the second `2 + 6 + 10 = 18`, and so on. The list `c` was longer (6 items), but `map` stopped after 4 because the shortest list, `a` (and `b`), ran out.

### Remember

- `map(function, iterable)` runs the function on **every item**, one at a time.
- Pass the function **without brackets**.
- It returns a **map object (iterator)**, so wrap it in `list()` to see the values.
- It saves you from writing a `for` loop each time.

## Day 3 – lambda

### What a lambda is

A **lambda** is a **small function written in a single line**, with **no name**. You can write it right where you need it, for example inside `map()`, instead of defining a separate function with `def` somewhere above.

The pattern is:

```python
lambda parameters: expression
```

- The word `lambda`, then the **parameters** (the inputs, separated by commas if there are several).
- A **colon `:`**.
- One **expression**, which is the result. A lambda **returns that result automatically**, so you don't write `return`.

> **In plain words:** a `def` function is a **named recipe card** you keep in a drawer. A lambda is a **sticky note** with a quick instruction, written on the spot, used once, and thrown away.

Here is the same function written both ways:

```python
def add5(x):
    return x + 5

add5_lambda = lambda x: x + 5

print(add5(1))
print(add5_lambda(1))
```

Output:

```text
6
6
```

Both do exactly the same thing. The lambda took one line instead of two.

A lambda can also be **called straight away** without giving it any name, or it can be saved in a variable (like `x` below) and called like a normal function:

```python
x = lambda a, b: a + b
print(x(4, 3))
print((lambda a, b: a * b)(4, 3))
```

Output:

```text
7
12
```

The first line saved the lambda in `x` and called it with `4` and `3`. The second wrapped the lambda in brackets and called it immediately, with no name at all.

### lambda with map()

The most common use of lambda is inside `map()`. Because the function is written right there, you don't need to define and name it first:

```python
lst = [1, 2, 3, 4, 5, 6]
print(list(map(lambda x: x + 5, lst)))
print(list(map(lambda x: x * x, lst)))
```

Output:

```text
[6, 7, 8, 9, 10, 11]
[1, 4, 9, 16, 25, 36]
```

Read the first line as: "for every `x` in `lst`, give back `x + 5`."

### Celsius and Fahrenheit with lambda

Before, we defined `celsius()` and `fahrenheit()` with `def` (several lines each) and then used `map`. With lambda, **both are done in one line each**, with no separate functions:

```python
temp = [0, 22.5, 40, 100]

c_temps = list(map(lambda T: (5/9) * (T - 32), temp))
print(c_temps)

print(list(map(lambda T: (9/5) * T + 32, c_temps)))
```

Output:

```text
[-17.77777777777778, -5.277777777777778, 4.444444444444445, 37.77777777777778]
[0.0, 22.5, 40.0, 100.0]
```

This gives exactly the same result as the `def` version, but instead of 5 or 6 lines of code, it is one line per conversion.

### lambda with more than one input

A lambda can take several parameters, and `map()` can be given one list for each of them:

```python
a = [1, 2, 3, 4]
b = [5, 6, 7, 8]
c = [9, 10, 11, 12, 4, 5]
print(list(map(lambda x, y, z: x + y + z, a, b, c)))
```

Output:

```text
[15, 18, 21, 24]
```

`x` takes its values from `a`, `y` from `b` and `z` from `c`. It stops after 4 results because the shortest list has 4 items.

### A lambda can have a condition

You can include a one-line `if ... else` inside the expression:

```python
print(list(map(lambda n: 'even' if n % 2 == 0 else 'odd', [1, 2, 3])))
```

Output:

```text
['odd', 'even', 'odd']
```

### Limits, and when to use lambda

- A lambda holds **only one expression**. You can't put several lines or several statements in it. For anything longer, use `def`.
- It has **no name**, so error messages and debugging are less clear. If you need to use the same function in many places, `def` is better.
- Use lambda for **short, one-off jobs**, especially as the function inside `map()` (and later `filter()` and `reduce()`).

|  | `def` function | `lambda` |
| --- | --- | --- |
| Has a name | Yes | No (anonymous) |
| Lines of code | One or many | One expression only |
| Needs `return` | Yes, to give a value back | No, the result is returned automatically |
| Best for | Reusable, longer logic | Short, quick, one-time use |

## Day 3 – reduce()

### What reduce does

`reduce(function, iterable)` takes a whole sequence and **boils it down to one single value**. It does this by applying a function that takes **two** values, over and over:

1. It takes the **first two** items and applies the function to them.
2. It takes that **result** together with the **third** item and applies the function again.
3. It keeps going, carrying the result forward, until **only one value is left**. That value is the answer.

> **In plain words:** `reduce` is a **snowball rolling down a hill**. It starts with the first two items, and each time it rolls it picks up the next item and gets bigger. At the bottom of the hill you have one big snowball, which is the single answer.

### The import

Unlike `map` and `filter`, `reduce` is not available by default. You have to import it first. You said "from tools import reduce", but the module is called **`functools`** ("function tools"):

```python
from functools import reduce
```

### Example: joining names

This is the notebook's example. It uses a lambda that adds (joins) two values:

```python
from functools import reduce

lst = ['kota', 'ruchik', 'joey', 'tribiani']
print(reduce(lambda a, b: a + b, lst))
```

Output:

```text
kotaruchikjoeytribiani
```

The lambda `lambda a, b: a + b` takes two things and joins them with `+`. Here is what `reduce` did, one step at a time:

```python
steps = lst[0]
for item in lst[1:]:
    steps = steps + item
    print(steps)
```

Output:

```text
kotaruchik
kotaruchikjoey
kotaruchikjoeytribiani
```

- Step 1: `'kota' + 'ruchik'` gives `'kotaruchik'`.
- Step 2: that result `+ 'joey'` gives `'kotaruchikjoey'`.
- Step 3: that result `+ 'tribiani'` gives `'kotaruchikjoeytribiani'`.

Four items went in and one value came out. In the notebook this is shown with a diagram (the sequence shrinking one step at a time until one value is left).

### The same idea with numbers

With numbers, `+` gives the total, and `*` gives the product:

```python
nums = [1, 2, 3, 4, 5]
print(reduce(lambda a, b: a + b, nums))
print(reduce(lambda a, b: a * b, nums))
```

Output:

```text
15
120
```

To *see* what `reduce` does with each pair, use a function that prints its two inputs. `a` is the **result so far** (the snowball) and `b` is the **next item**:

```python
def show(a, b):
    print('a =', a, ' b =', b, ' ->', a + b)
    return a + b

print(reduce(show, nums))
```

Output:

```text
a = 1  b = 2  -> 3
a = 3  b = 3  -> 6
a = 6  b = 4  -> 10
a = 10  b = 5  -> 15
15
```

The `a` of each row is the answer of the row before it.

### Example: finding the maximum

The notebook's second example finds the biggest number. The function takes two numbers and keeps the bigger one:

```python
max_find = lambda a, b: a if a > b else b
l2 = [47, 49, 42, 55, 56]
print(reduce(max_find, l2))
print(max(l2))
```

Output:

```text
56
56
```

The winner is carried forward at each step: 47 vs 49 gives 49, then 49 vs 42 gives 49, then 49 vs 55 gives 55, then 55 vs 56 gives 56. Python already has a built-in `max()` for this (it gives the same `56`), so the example is only to show how `reduce` works.

### Starting value

You can give `reduce` a third argument, a **starting value**, which is used as the first `a`. It also makes `reduce` safe on an empty list:

```python
print(reduce(lambda a, b: a + b, nums, 100))

try:
    reduce(lambda a, b: a + b, [])
except TypeError as e:
    print(e)

print(reduce(lambda a, b: a + b, [], 0))
```

Output:

```text
115
reduce() of empty iterable with no initial value
0
```

## Day 3 – filter()

### What filter does

`filter(function, iterable)` goes through every item and **keeps only the ones for which the function gives `True`**. The function must give a yes/no (True/False) answer for each item. Items that get `True` are kept. Items that get `False` are thrown away.

> **In plain words:** `filter` is a **sieve** (or a bouncer at a door). Every item walks up, the function asks "are you allowed in?", and only the ones that get a yes come through.

### Example: keep the even numbers

First, a function that says whether a number is even (`% 2 == 0` means it divides by 2 with nothing left over):

```python
def even_check(num):
    if num % 2 == 0:
        return True

print(even_check(8))
print(even_check(7))
```

Output:

```text
True
None
```

For 7 the function never reaches a `return`, so it gives `None`. `filter` treats `None` as "no" (it counts as false), so this works, but it is cleaner to return `True` or `False` every time (`return num % 2 == 0`).

Now hand the function to `filter` along with the list. As with `map`, pass the function **without brackets**:

```python
lst = [1, 2, 3, 4, 5, 6, 7, 8]
print(list(filter(even_check, lst)))
```

Output:

```text
[2, 4, 6, 8]
```

Only the numbers for which `even_check` said `True` are in the result.

**filter gives an iterator too.** Just like `map`, `filter` returns a **filter object** (an iterator), so wrap it in `list()`, and it can be used only once:

```python
f = filter(even_check, lst)
print(type(f))
print(list(f))
print(list(f))
```

Output:

```text
<class 'filter'>
[2, 4, 6, 8]
[]
```

### filter with lambda

For a quick job you don't need to write a separate function. Use a lambda:

```python
print(list(filter(lambda x: x % 2 == 0, lst)))
```

Output:

```text
[2, 4, 6, 8]
```

**filter vs map.** This is a common mix-up. The notebook has a cell that uses `map` with the same lambda. Compare them:

```python
print(list(filter(lambda x: x % 2 == 0, lst)))
print(list(map(lambda x: x % 2 == 0, lst)))
```

Output:

```text
[2, 4, 6, 8]
[False, True, False, True, False, True, False, True]
```

- `filter` **keeps the items** that pass the test.
- `map` **transforms every item** into the test's answer (`True` or `False`), so you still get all 8 values.

### Example: words longer than 6 letters

```python
words = ['ruchi', 'Nikhil', 'phoebee', 'swapna']
long_words = list(filter(lambda word: len(word) > 6, words))
print(long_words)
```

Output:

```text
['phoebee']
```

The lengths are 5, 6, 7 and 6. Only `'phoebee'` (7 letters) is longer than 6. With `len(word) > 5`, the three words with 6 or more letters would pass:

```python
print(list(filter(lambda word: len(word) > 5, words)))
```

Output:

```text
['Nikhil', 'phoebee', 'swapna']
```

### map, filter and reduce together

|  | Takes | Gives back | Think of it as |
| --- | --- | --- | --- |
| `map(f, items)` | a function and items | **Every** item, changed by `f` (same count as the input) | a stamp |
| `filter(f, items)` | a function that says True/False, and items | **Only some** of the items (those that got `True`) | a sieve |
| `reduce(f, items)` | a function of **two** values, and items | **One** single value | a snowball |

`map` and `filter` are always available. `reduce` has to be imported with `from functools import reduce`. All three are very often written with a **lambda**.

## Comparing strings, lists, tuples, sets and dictionaries

These are the five main "containers" (ways to hold data) in Python. This one table puts them side by side so you can see what is the same, what is different, and which to pick.

> **In plain words:** think of five kinds of storage. A **string** is a necklace of letters. A **list** is an open backpack. A **tuple** is a sealed box. A **set** is a bag of unique marbles. A **dictionary** is a phone book. Each one is good at a different job.

|  | **String** | **List** | **Tuple** | **Set** | **Dictionary** |
| --- | --- | --- | --- | --- | --- |
| **Looks like** | `'hello'` | `[1, 2, 3]` | `(1, 2, 3)` | `{1, 2, 3}` | `{'a': 1, 'b': 2}` |
| **Empty one** | `''` | `[]` | `()` | `set()` | `{}` |
| **What it holds** | Text (characters only) | Any items, in order | Any items, in order | Unique items | Key : value pairs |
| **Mutable (can be changed)?** | No | **Yes** | No | **Yes** | **Yes** |
| **Keeps order / has index positions?** | Yes | Yes | Yes | No | By key, not by position\* |
| **Indexing and slicing?** | Yes | Yes | Yes | No | No (use the key) |
| **Allows duplicates?** | Yes | Yes | Yes | No (all unique) | Values yes, keys no |
| **Can mix data types?** | No (only characters) | Yes | Yes | Yes (if hashable) | Yes |
| **Stored using** | Sequence | Sequence | Sequence | Hash table | Hash table |
| **Finding a value** | By index | By index (`in` checks every item) | By index | `in` is very fast | By key, very fast |
| **Can be a dictionary key / set member?** | Yes | No | Yes (if its items are) | No | No |
| **Approx. number of methods** | **Most (about 47)** | About 11 | **Fewest (2)** | About 17 | About 11 |
| **Advantages** | Rich set of text tools (`upper`, `split`, `replace`, `strip`...). Safe: nobody can change it by mistake. | Flexible: grow, shrink, sort, change. Keeps order. The all-purpose container. | Safe: can't be changed by mistake. Slightly lighter and faster than a list. Can be used as a dictionary key. | Removes duplicates automatically. Very fast "is it in here?" checks. Has set maths (union, intersection, difference). | Meaningful names for data (`'age'` instead of position 3). Very fast lookups. Easy to nest. |
| **Disadvantages** | Can't edit a character in place, every change builds a new string. Only for text. | Slower to search a big list. Anyone can change it, so it is less safe. Allows duplicates you may not want. | Can't add, remove or change items. Very few methods. | No order, no indexing or slicing. Items must be unchangeable (hashable). Can't hold duplicates. | Takes more memory. Keys must be unique and immutable. Not accessed by position. |
| **How often used in development** | **Very high** | **Very high** | Medium (lower than list) | **Lowest of the five** | **Very high** |
| **Where it is mostly used** | Names, messages, file paths, user input, reading and cleaning text data. | Collections of records, results of loops, rows of data, anything you need to grow and change. | Fixed data: coordinates, days of the week, RGB colours, returning several values from a function. | Removing duplicates, membership checks, comparing two groups of data. | JSON and API data, configuration settings, counting things, lookups (id to name), records with named fields. |

\* Dictionaries do remember the order you added items in (in current Python versions), but you can't use a number position like `d[0]` to reach an item. You reach it by its key. Method counts are for the public methods of each type in current Python and can change a little between versions.

### Quick answers to your questions

- **Most used in development:** strings, lists and dictionaries. Almost every program uses all three. Dictionaries in particular are everywhere because JSON data from the web and APIs looks like a dictionary.
- **Least used in development:** sets, then tuples. They are used for specific jobs (removing duplicates, fixed data), not as the default container.
- **Most methods:** strings (about 47), because they come with many text tools. **Fewest methods:** tuples (only `index` and `count`).
- **Can be changed after creation:** lists, sets, dictionaries. **Cannot be changed:** strings and tuples.
- **Keep their order:** strings, lists and tuples (these are the *sequences*).
- **Guarantee uniqueness:** sets (all values) and dictionaries (the keys).

### Which one should I use?

| If you need to... | Use a |
| --- | --- |
| store text | string |
| keep an ordered collection that you will add to, remove from or sort | list |
| store a fixed group of values that must never change | tuple |
| remove duplicates or check quickly whether something exists | set |
| look something up by a name or an ID | dictionary |

### Converting between them

You can switch from one container to another with their names: `list()`, `tuple()`, `set()`, `str()` and `dict()`. This is the same "convert, change, convert back" idea you used to change a tuple.

```python
items = [3, 1, 2, 3, 1]
print(set(items))
print(tuple(items))
print(list('abc'))
print(dict([('a', 1), ('b', 2)]))
print(sorted(set(items)))
```

Output:

```text
{1, 2, 3}
(3, 1, 2, 3, 1)
['a', 'b', 'c']
{'a': 1, 'b': 2}
[1, 2, 3]
```

`set(items)` drops the duplicates, `tuple(items)` freezes the list, `list('abc')` splits a string into letters, `dict(...)` builds a dictionary from pairs, and `sorted(set(items))` removes duplicates and puts the result in order as a list.

## Day 3 – In my own words (what I understood)

- **Tuple** `( )`: a container that cannot be changed (immutable). It allows duplicates and keeps order, so indexing and slicing work like a list. To "change" it, turn it into a list, edit the list, and turn it back into a tuple. It has only two methods: `.index()` and `.count()`.
- **Set** `{ }`: stores unique values in a hash table, so there is no order, no indexing and no slicing. I add with `add()`, delete with `remove()` / `discard()` / `pop()`, and empty it with `clear()`.
- **Dictionary** `{key: value}`: also a hash table. I reach a value by its **key**, not by position. Keys are unique, values can repeat. Dictionaries can be nested, and I can change values with `+=` / `-=`. A real copy needs `copy.copy()` (shallow) or `copy.deepcopy()` (deep). `keys()`, `values()` and `items()` let me look inside.
- **Function** `def`: runs a group of statements when I call it. `print` only shows something, `return` hands a value back so I can use it.
- **Iterator / generator:** `iter()` and `next()` give one item at a time; a generator does the same with `yield` and is the version used in real projects, because it never builds the whole list in memory.
- **`map`** applies a function to every item, **`filter`** keeps the items that pass a test, **`reduce`** (from `functools`) squeezes everything into one value, and **`lambda`** is a quick one-line function that I can pass into any of these.

## Day 3 – Extras from the notebook (not covered in class)

### Dictionary comprehension

Just like a list comprehension, but it builds a dictionary: `{key: value for ... in ...}`.

> **In plain words:** it is a one-line recipe that says "for each item, make this key and this value", instead of writing a loop and adding pairs one by one.

```python
squares = {x: x**2 for x in range(1, 6)}
print(squares)
lengths = {w: len(w) for w in ['apple', 'kiwi', 'banana']}
print(lengths)
flipped = {v: k for k, v in lengths.items()}
print(flipped)
```

Output:

```text
{1: 1, 2: 4, 3: 9, 4: 16, 5: 25}
{'apple': 5, 'kiwi': 4, 'banana': 6}
{5: 'apple', 4: 'kiwi', 6: 'banana'}
```

The last line swaps keys and values. Be careful: if two values were the same, one would overwrite the other, because keys must be unique.

### A note on dictionary keys

The notebook points out that keys are harder to organise than values, because key names are not based on the data itself and you have to decide and remember them. A good habit is to pick short, consistent key names (all lowercase, same style) so the dictionary stays easy to read.
