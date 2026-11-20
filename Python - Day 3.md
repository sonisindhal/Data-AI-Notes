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
