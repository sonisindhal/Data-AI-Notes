# Python Day 1

Nov 19, 2026 · @Soni Sindhal

## Day 1 – Python Basics (Session 1)

### What Python is and how to run it

Python is a high-level, dynamically typed language that reads almost like plain English, so you can express a lot in very few lines.

> **In plain words:** Python is a language for giving a computer step-by-step instructions. The computer does exactly what you write, nothing more and nothing less. (The snake is only the name. It comes from a comedy show, Monty Python.)

Three ways to write and run Python, as covered in class:

1. **Jupyter**: use it directly, writing code in cells and running them one at a time.
2. **Anaconda**: a toolbox that bundles Python, Jupyter and other tools together.
3. **Visual Studio Code**: the editor the instructor recommended using.

To check which version is installed, run `!python --version` in a Jupyter cell. Mine showed Python 3.13.9.

```python
!python --version
```

Output:

```text
Python 3.13.9
```

### print() and automatic type detection

`print()` shows whatever you give it, text or numbers, with no setup. Python works out the type by itself, so you never declare a string or an integer first.

```python
print('hello Joeyyy!')   # text
print(123)               # integer
```

Output:

```text
hello Joeyyy!
123
```

In Jupyter, writing a bare value on the last line of a cell (like `123`) also shows it. `print()` is what you use when you want output from anywhere in the code.

Compare with Java, where the same hello-world needs a class, a `main` method and `System.out.println`. In Python it is one line.

### Integers and variables

An integer is any whole number with no decimal part, like `9` or `-3`. A variable is created just by assigning a value to it: `a = 9`.

A variable always holds its **current** value, never the previous one. Each new assignment replaces the old one.

> **In plain words:** think of a variable as a **labelled box**. The label is the name (`a`) and the box holds a value (`9`). If you put a new value in the same box, the old one is gone. The box only ever holds its latest value.

```python
a = 1
print(a)
a = 5
print(a)
```

Output:

```text
1
5
```

Because Python is dynamically typed, a variable is just a label pointing at a value. The same label can later point at a different type:

```python
tenth = 10
print(tenth, type(tenth))
tenth = 15.9
print(tenth, type(tenth))
tenth = 'ten'
print(tenth, type(tenth))
```

Output:

```text
10 <class 'int'>
15.9 <class 'float'>
ten <class 'str'>
```

### Type casting

Casting means changing a value from one data type to another. There are two kinds:

- **Implicit**: Python converts the type automatically.
- **Explicit**: you tell Python which type you want, using a function like `str()`.

**Implicit example.** Adding an int and a float gives a float, with no work from you:

```python
x = 5          # int
y = 1.234      # float
z = x + y      # Python makes the result a float
print(z)
print(type(z))
```

Output:

```text
6.234
<class 'float'>
```

**Explicit example.** To join a number onto a string, convert the number to a string first. Without it, Python raises a `TypeError`:

```python
a = 7
print("text" + str(a))   # works
print("text" + a)        # fails
```

Output:

```text
text7
TypeError: can only concatenate str (not "int") to str
```

Python is strongly typed, so it will not guess in a case like this. The type of a value matters, and you convert it yourself when needed.

> **In plain words:** `'5'` in quotes is just the *text* "5", like the written word. `5` is a real number you can add up. Casting (`int('5')`) turns the text into the real number so you can calculate with it.

### Booleans

A boolean can only be `True` or `False`, written without quotes and with a capital first letter.

> **In plain words:** a boolean is a **light switch**. It is either `True` (on) or `False` (off), with nothing in between. Python uses it to answer yes/no questions.

```python
b1 = True
b2 = False
print(b1, b2)
print(type(b2))
```

Output:

```text
True False
<class 'bool'>
```

### Strings and quotes

A string is text. You can write it with single quotes (`'...'`), double quotes (`"..."`) or triple quotes (`'''...'''` or `"""..."""`). The quote you choose matters when the text itself contains quotes.

> **In plain words:** a string is just **text**. Whenever you put something inside quote marks, Python treats it as text, even if it looks like a number.

**Four ways to combine quotes in a string:**

1. **Single quote inside the text:** wrap the string in double quotes.

   ```python
   s1 = "joy's and ravi's book"
   print(s1)
   ```

   Output:

   ```text
   joy's and ravi's book
   ```
2. **Double quotes inside the text:** wrap the string in single quotes.

   ```python
   s2 = 'He said "hello" and "bye"'
   print(s2)
   ```

   Output:

   ```text
   He said "hello" and "bye"
   ```
3. **Both kinds of quotes inside the text:** wrap the string in triple quotes.

   ```python
   s3 = '''ravi's note: "don't forget"'''
   print(s3)
   ```

   Output:

   ```text
   ravi's note: "don't forget"
   ```
4. **Escape the quote with a backslash `\`:** this lets you use the same quote type inside and outside.

   ```python
   s4 = 'joy\'s and ravi\'s book'
   s5 = "He said \"hello\""
   print(s4)
   print(s5)
   ```

   Output:

   ```text
   joy's and ravi's book
   He said "hello"
   ```

\
print s4\


The backslash `\` (it leans backwards) is different from the forward slash `/`. A backslash before a character tells Python to treat that character as part of the text, not as the end of the string.

Triple-quoted strings can also span several lines.

If you write `'ruchik's kota'` with no escape, Python thinks the string ends at the second `'` and raises a `SyntaxError`.

### Naming rules for variables

A variable name can only use **letters, digits and the underscore `_`**. Three rules follow from that:

1. **It must not start with a number.** `name1` is fine, but `1name` is not. Digits are allowed after the first character.
2. **It must not start with a special character**, such as `%`, `@`, `-` or `$`. These symbols already have a meaning in Python (for example `%` is the remainder operator), so they can't be part of a name. The underscore `_` is the only special character allowed.
3. **It must not reuse a built-in name** such as `str`, `list`, `print` or `int`. If you want a name like that, put an underscore **in front of it** (`_str`) so it stays different from the built-in.

Names are also case-sensitive, so `age` and `Age` are different variables.

> **In plain words:** these are the rules for what you may call your "box". Python already uses some names itself (like `str` and `print`), so if you reuse one you break the original. An underscore in front (`_str`) keeps your name separate.

**Valid names:**

```python
name1 = 5
print(name1)

user_name = 'joy'
print(user_name)

_str = 'ruchik'     # underscore keeps it different from the built-in str
print(_str)

age = 1
Age = 2
print(age, Age)
```

Output:

```text
5
joy
ruchik
1 2
```

**Invalid names:**

```python
1name = 5
```

Output:

```text
SyntaxError: invalid decimal literal
```

```python
user@name = 1
```

Output:

```text
SyntaxError: cannot assign to expression here. Maybe you meant '==' instead of '='?
```

**Why rule 3 matters.** If you reuse a built-in name, the built-in stops working (in Jupyter, restart the kernel to fix it):

```python
str = "hello"
print(str)
print(str(5))
```

Output:

```text
hello
TypeError: 'str' object is not callable
```

With an underscore in front, both names work side by side:

```python
_str = "hello"
print(_str)
print(str(5))
```

Output:

```text
hello
5
```

### Floats and complex numbers

A **float** is a number with a decimal part, like `1.234`. A **complex** number is written `x + yj`, where `j` marks the imaginary part.

```python
y = 1.234
print(y, type(y))

j = 1.0 - 2.0j
print(j, type(j))
print(j.real, j.imag)
```

Output:

```text
1.234 <class 'float'>
(1-2j) <class 'complex'>
1.0 -2.0
```

You can check any value's type with `type()`.

**Note:** complex numbers are mainly used in vectorization and image data, mostly in the neural network part. The instructor said to ignore them for now and not spend much time on them.

### Dynamic typing (duck typing)

When you assign a value to a variable, Python decides the variable's type from that value. You never declare a type. This is called **dynamic typing**, and the instructor also called it duck typing.

> **In plain words:** in some languages you have to say "this box only holds numbers" before you use it. Python doesn't ask. It looks at what you put in the box and works out the type by itself, and you can put something of a different type in the same box later.

```python
ten = 10
print(type(ten))

ten = 'ten'
print(type(ten))
```

Output:

```text
<class 'int'>
<class 'str'>
```

The first time, `ten` holds `10`, so `type(ten)` is `int`. After `ten = 'ten'`, the same variable holds text, so `type(ten)` is `str`. The variable takes on whatever type of value it was last given.

Strictly speaking, duck typing is the related idea that Python cares about what an object can do rather than what type it is. In class the two names were used for the same behaviour, so treat them as one for now.

### Operators

**Arithmetic**, shown with `a = 10` and `b = 4`:

| Operator | Meaning | Example | Result |
| --- | --- | --- | --- |
| `+` | add | `a + b` | 14 |
| `-` | subtract | `a - b` | 6 |
| `*` | multiply | `a * b` | 40 |
| `/` | divide (always gives a float) | `a / b` | 2.5 |
| `%` | remainder (modulo) | `a % b` | 2 |
| `**` | power | `a ** b` | 10000 |
| `//` | floor division (drops the decimal) | `a // b` | 2 |

**The three operators that are easy to mix up:**

- `%` is **modulo**. It gives the **remainder** after dividing. It is often used to check even or odd: `n % 2` is `0` for even numbers and `1` for odd numbers.
- `**` is **power**. `a ** b` means a to the power of b. A square is `** 2`, a cube is `** 3`.
- `//` is **floor division**. It divides and keeps only the whole-number part, rounding down. It does not give the denominator. The denominator is the bottom number of a division (the `4` in `10 / 4`).

```python
print(10 / 4)     # normal division
print(10 // 4)    # floor division: whole part only
print(10 % 4)     # remainder
print(5 ** 2)     # square
print(5 ** 3)     # cube
print(-7 // 2)    # rounds down, so -3.5 becomes -4
print(9 % 2)      # 1 means odd
```

Output:

```text
2.5
2
2
25
125
-4
1
```

`10 / 4` is 2.5. `10 // 4` keeps the 2, and `10 % 4` is the 2 left over.

> **In plain words:** share 10 sweets between 4 kids. `/` says each gets 2.5 sweets, `//` says each gets 2 *whole* sweets, and `%` says 2 sweets are *left over*.

**Comparison** operators give `True` or `False`: `==` (equal), `!=` (not equal), `<`, `>`, `<=`, `>=`.

| Meaning | Maths symbol | Python | Example with `a = 5`, `b = 7` | Result |
| --- | --- | --- | --- | --- |
| equal to | = | `==` | `a == b` | False |
| not equal to | ≠ | `!=` | `a != b` | True |
| greater than | > | `>` | `a > b` | False |
| less than | < | `<` | `a < b` | True |
| greater than or equal to | ≥ | `>=` | `a >= b` | False |
| less than or equal to | ≤ | `<=` | `a <= b` | True |

In Python, "equal to" is written with **two** equals signs (`==`). A single `=` assigns a value. The symbols ≠, ≥ and ≤ can't be typed in code, so use `!=`, `>=` and `<=`.

> **In plain words:** one `=` is an *order* ("put this in the box"). Two `==` is a *question* ("are these the same?"), and the answer is `True` or `False`.

```python
a = 5
b = 7
print(a == b)
print(a != b)
print(a > b)
print(a < b)
print(a >= b)
print(a <= b)
```

Output:

```text
False
True
False
True
False
True
```

**Logical** operators combine booleans: `and` is True only if both sides are True, `or` is True if at least one is, and `not` flips the value.

> **In plain words:** `and` means *both* things must be true ("I have my ticket **and** my ID"). `or` means *at least one* must be true. `not` flips the answer.

```python
x = True
y = False
print(x and y)
print(x or y)
print(not y)
print(not x)
```

Output:

```text
False
True
True
False
```

All four combinations of two booleans:

| `x` | `y` | `x and y` | `x or y` |
| --- | --- | --- | --- |
| True | True | True | True |
| True | False | False | True |
| False | True | False | True |
| False | False | False | False |

Note that `True` and `False` must start with a capital letter. Writing `false` in lowercase gives a `NameError`.

**Assignment** operators update a variable: `x += 5` means `x = x + 5`, and `x -= 5` means `x = x - 5`.

```python
x = +5
print(x)

x = -5
print(x)

x += 5      # same as x = x + 5
print(x)

x -= 5      # same as x = x - 5
print(x)
```

Output:

```text
5
-5
0
-5
```

Step by step: `x = +5` makes `x` equal to 5, and `x = -5` makes it -5. The `+` and `-` here are just the sign of the number. `x = +5` does **not** mean 5 + 5.

Then `x += 5` adds 5 to the current value (-5 + 5 = 0), and `x -= 5` subtracts 5 from it (0 - 5 = -5).

The same shortcut works for the other arithmetic operators: `*=`, `/=`, `//=`, `%=` and `**=`.

One `=` **assigns** a value (`a = 5`). Two `==` **compares** two values (`a == 5`).

All the operators together, with `a = 10` and `b = 4`:

```python
a = 10
b = 4
print(a + b, a - b, a * b, a / b, a % b, a ** b, a // b)   # arithmetic
print(a == b, a != b, a < b, a > b, a <= b, a >= b)         # comparison
print(True and False, True or False, not False)             # logical

x = 5
x += 5
print(x)
x -= 3
print(x)
```

Output:

```text
14 6 40 2.5 2 10000 2
False True False True False True
False True True
10
7
```

### input(), f-strings and .format()

**`input()`** lets the user type a value while the program runs. You store it in a variable, for example `name = input("...")`. The text inside the quotes is the message shown to the user. Whatever the user types is saved in the variable, and you can then use it in a `print`.

```python
name = input("Enter your name: ")
print("Hello", name)
print(type(name))
```

Output (the user types `Joey`):

```text
Enter your name: Joey
Hello Joey
<class 'str'>
```

The user can type text or a number, but `input()` **always gives back a string**, even when a number is typed:

> **In plain words:** `input()` makes the program stop and ask the user a question. Whatever they type comes back as **text**, even if they typed a number. If you want to do maths with it, change it to a number first with `int()`.

```python
age = input("Enter your age: ")
print(age, type(age))
```

Output (the user types `25`):

```text
Enter your age: 25
25 <class 'str'>
```

If you need a number to do maths with, convert it with `int()`:

```python
age = int(input("Enter your age: "))
print(age + 1)
```

Output (the user types `25`):

```text
Enter your age: 25
26
```

**f-strings** let you put variables straight into a sentence. Write an `f` before the opening quote and put each variable name inside curly brackets `{}`. Python replaces each `{variable}` with its value.

> **In plain words:** an f-string is a **fill-in-the-blanks sentence**. You write the sentence once with `{}` holes, and Python fills each hole with the value of a variable.

```python
age = 57
print(type(age))
age = 97               # the variable now holds the latest value
year = 1974
x = f"I am {age} years old, born in {year}"
print(x)
```

Output:

```text
<class 'int'>
I am 97 years old, born in 1974
```

**`.format()`** is the other way. Put placeholders `{0}`, `{1}` in the text, then give the values inside `.format(...)`. The number in the brackets is the **position** of the value: `{0}` is the first value, `{1}` is the second.

```python
language_1 = "tel"
subject = "telugu"
print("I love {0}, my subject is {1}".format(language_1, subject))
```

Output:

```text
I love tel, my subject is telugu
```

The numbers decide which value goes where, so swapping them swaps the values. Using the same number twice prints the same value twice:

```python
print("I love {1}, my subject is {0}".format(language_1, subject))
print("I love {0}, my subject is {0}".format(language_1, subject))
print("I love {1}, my subject is {1}".format(language_1, subject))
```

Output:

```text
I love telugu, my subject is tel
I love tel, my subject is tel
I love telugu, my subject is telugu
```

f-strings are shorter and more common, but `.format()` is worth knowing because you will see it in other people's code.

### Branching: if / elif / else

Branching lets the program choose what to run based on a condition. Python checks the conditions from top to bottom and runs only the **first** block that is True. If none are True, the `else` block runs.

> **In plain words:** branching is a **fork in the road**. *If* it is raining, take an umbrella. *Else if* it is sunny, wear a hat. *Else*, just go. Python checks the questions from the top and takes only the first road whose answer is yes.

```python
i = 4

if i < 3:
    print('value is less than 3')
    if i < 2:                      # nested if, one level deeper
        print('less than 3 and 2')
elif i < 5:
    print('less than 5')           # this one runs
elif i < 12:
    print('less than 12')
else:
    print('12 or more')
```

Output:

```text
less than 5
```

The keywords are `if`, `elif` (short for "else if") and `else`. The `else` block has no condition. It runs only when none of the conditions above it were True. A nested `if` is an `if` inside another `if`, and it is only checked when the outer condition is True.

Trying several values of `i` shows which branch runs each time:

```python
for i in [1, 2, 4, 20]:
    print("i =", i)
    if i < 3:
        print('  less than 3')
        if i < 2:                  # nested if
            print('  less than 2')
    elif i < 5:
        print('  less than 5')
    else:
        print('  5 or more')
```

Output:

```text
i = 1
  less than 3
  less than 2
i = 2
  less than 3
i = 4
  less than 5
i = 20
  5 or more
```

Points to remember:

- The condition ends with a colon `:`.
- **Indentation** shows which lines belong to the block. Python uses it instead of curly braces.
- `elif` and `else` are optional.
- Any value can be a condition. `0`, `None` and empty values count as False, and everything else counts as True.

### Loops

A loop repeats a task, so you don't have to write the same code again and again. Python has two loops:

> **In plain words:** a loop is a way to **repeat** something without writing it again and again. Instead of printing "hello" 100 times by hand, you tell Python "do this 100 times".

- **`for` loop:** use it when you **know how many times** you want to repeat, or what you want to go through (a list, a string, or a range of numbers).
- **`while` loop:** use it when you **don't know in advance** how many times it needs to repeat. It keeps going for as long as a condition is True.

### for loops

A `for` loop goes through a sequence one item at a time and stops after the last item. The loop body is indented. With `range(5)` the loop runs 5 times, for 0, 1, 2, 3 and 4, and then it ends. It stops *before* 5, not at 5 (more on this under `range()` below).

> **In plain words:** a `for` loop says "for every item in this group, do this". The loop variable (`i`) is the item you are holding right now. It changes to the next item each time round.

**1. Sum the numbers in a list:**

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11]
summ = 0
for i in numbers:
    summ += i          # same as summ = summ + i
print(summ)
```

Output:

```text
66
```

**2. Join strings with `+`.** When you work with strings, you use the plus sign to concatenate them. Adding a string at the end keeps the order, and adding it in front reverses the order:

```python
names = ["joey", "ruchik", "kota"]
summ = ''
rev = ''
for i in names:
    summ = summ + ' ' + i
    rev = " " + i + rev
print(summ)
print(rev)
```

Output (each line starts with a space):

```text
 joey ruchik kota
 kota ruchik joey
```

**3. Index and value** with `range(len(...))`:

```python
char = [1, 32, 5]
for i in range(len(char)):
    print(f"index {i} has value {char[i]}")
```

Output:

```text
index 0 has value 1
index 1 has value 32
index 2 has value 5
```

**4. A string is a sequence too.** Print each letter with its index:

```python
s = 'Jimhalpertt'
for i in range(len(s)):
    x = f'{i},{s[i]}'
    print(x)
```

Output:

```text
0,J
1,i
2,m
3,h
4,a
5,l
6,p
7,e
8,r
9,t
10,t
```

**5. Reverse a string** by adding each letter in front of the result:

```python
s = 'chandler'
x = ''
for i in range(len(s)):
    x = s[i] + x
print(x)
```

Output:

```text
reldnahc
```

### range(): lower limit, upper limit and step size

`range()` gives a sequence of numbers and takes three parameters, `range(lower limit, upper limit, step size)`:

> **In plain words:** `range()` is a **counting machine**. `range(1, 10, 3)` means "start at 1, stop before 10, jump 3 each time", so it counts 1, 4, 7. The stopping number is never included.

| Parameter | Meaning | Default |
| --- | --- | --- |
| Lower limit | the number to start from (**included**) | 0 |
| Upper limit | the number to stop at (**not included**) | required |
| Step size | the gap between one number and the next | 1 |

With a single number, `range(5)`, that number is the upper limit, so you get 0, 1, 2, 3, 4. Wrap `range` in `list()` to see all its values at once.

**With a step size of 3.** Start at 2, stop before 20, jump by 3:

```python
print(list(range(2, 20, 3)))

for i in range(2, 20, 3):
    print(i)
```

Output:

```text
[2, 5, 8, 11, 14, 17]
2
5
8
11
14
17
```

The last value is 17, because the next one (20) is the upper limit and is not included.

**The upper limit is never printed.** If you want the numbers 0 to 9, `range(0, 9)` stops at 8. To include 9, add **+1** to the upper limit:

```python
lower = 0
upper = 9
print(list(range(lower, upper)))        # without +1
print(list(range(lower, upper + 1)))    # with +1
```

Output:

```text
[0, 1, 2, 3, 4, 5, 6, 7, 8]
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

The same thing with a lowest limit of 1, a highest limit of 10 and a step size of 1:

```python
lowest = 1
highest = 10
print(list(range(lowest, highest, 1)))        # without +1
print(list(range(lowest, highest + 1, 1)))    # with +1
```

Output:

```text
[1, 2, 3, 4, 5, 6, 7, 8, 9]
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

**When to add +1.** Add it when you are counting with numbers and you want the highest number itself to be included. Don't add it when you use `range` to go through the **index** of a list or string. `range(len(s))` already gives every index (0 up to the last one), so `+1` would go one past the end and fail:

```python
s = 'abc'
for i in range(len(s)):
    print(i, s[i])      # all three letters, no +1 needed

for i in range(len(s) + 1):
    print(i, s[i])      # one index too many
```

Output:

```text
0 a
1 b
2 c
0 a
1 b
2 c
IndexError: string index out of range
```

**A negative step size counts down.** Start at the last index, stop before -1, and jump by -2:

```python
genre = ['pop', 'pizza', 'jazz', 'swapna', 'joey', 'bing', 'kota']
for i in range(len(genre) - 1, -1, -2):
    print("I like", genre[i])
```

Output:

```text
I like kota
I like joey
I like jazz
I like pop
```

### while loops

A `while` loop keeps running **as long as its condition is True**. Use it when you don't know in advance how many times you need to repeat. The condition is checked before every pass, and if it is False at the start, the body never runs.

> **In plain words:** a `while` loop is like **stirring soup until it is hot**. You don't know how many stirs it will take, you just keep going *while* the answer to a question is yes. You must change something inside the loop, otherwise the answer never changes and the loop never stops.

```python
n = 5
summ = 0
i = 1                  # counter
while i <= n:
    summ = summ + i
    i = i + 1          # update the counter, or the loop never ends
print("The sum is", summ)
```

Output:

```text
The sum is 15
```

```python
count = 10
while count >= 0:
    print("Countdown:", count)
    count -= 1
print('happy new year')
```

Output:

```text
Countdown: 10
Countdown: 9
Countdown: 8
Countdown: 7
Countdown: 6
Countdown: 5
Countdown: 4
Countdown: 3
Countdown: 2
Countdown: 1
Countdown: 0
happy new year
```

Three things every `while` loop needs: a starting value, a condition, and a line inside the loop that changes the value. Without that last one you get an infinite loop.

**How a `while` loop runs:**

1. Python checks the condition.
2. If it is True, the indented body runs once. If it is False, the loop ends and Python moves on to the next line after the loop.
3. Python goes back to step 1 and checks the condition again.

The body is the indented block, and the first line that is not indented ends the loop. Any non-zero number counts as True, while `0` and `None` count as False.

**Print the even numbers from 2 to 10**, going up by 2 each time:

```python
i = 2
while i <= 10:
    print(i)
    i += 2
```

Output:

```text
2
4
6
8
10
```

**Go through a string** one letter at a time, using the index `i` and `len()` to know when to stop:

```python
s = 'ruchikkota'
i = 0
while i < len(s):
    print(s[i])
    i += 1
```

Output:

```text
r
u
c
h
i
k
k
o
t
a
```

**Looping until the user gives the right answer** with `while True` and `break`:

```python
name = 'stop'
while True:
    user_input = input("enter your name: ")
    if user_input == name:
        print("name matched, breaking")
        break
    else:
        print("name didn't match... keep entering the names")
```

Output (the user types `abc`, then `xyz`, then `stop`):

```text
enter your name: abc
name didn't match... keep entering the names
enter your name: xyz
name didn't match... keep entering the names
enter your name: stop
name matched, breaking
```

**`for` or `while`?** Use `for` when you know what to loop over, and `while` when you loop until a condition changes.

### break and continue

These two change how a loop runs.

> **In plain words:** `break` means "stop the whole loop now and leave". `continue` means "skip the rest of this round and start the next one". The loop keeps going.

- **`break`** ends the whole loop right away. In nested loops it ends only the innermost one.
- **`continue`** skips the rest of the current pass and moves on to the next item.

```python
for val in "string":
    if val == "i":
        break          # stop at the first 'i'
    print(val)
print("The end")

for val in "strinnnkig":
    if val == "i":
        continue       # skip every 'i', keep going
    print(val)
print("The end")
```

Output:

```text
s
t
r
The end
s
t
r
n
n
n
k
g
The end
```

Both work the same way in a `while` loop. Here the loop counts from 1 to 10, skips 5 with `continue`, and stops completely at 8 with `break`:

```python
i = 0
while i < 10:
    i += 1
    if i == 5:
        continue      # skip 5: go straight back to the while check
    if i == 8:
        break         # at 8: leave the loop completely
    print(i)
print("The end")
```

Output:

```text
1
2
3
4
6
7
The end
```

In a `while` loop, update the counter **before** the `continue`. Otherwise the counter never changes and the loop runs forever.

**The difference:**

|  | `break` | `continue` |
| --- | --- | --- |
| What it does | ends the loop completely | skips only the current pass |
| Where the program goes next | the first line after the loop | back to the loop check, for the next pass |
| Does the loop keep running? | no | yes, until its condition is False or the items run out |

### PS notes

Three small things the instructor mentioned along the way:

**1. Comments with `#`.** A comment is a note for the reader. Python ignores everything after the `#` on that line. It can sit on its own line or after some code. The instructor mentioned `##`, which also works, because the second `#` is simply part of the comment text. A single `#` is enough.

```python
# this whole line is a comment
print("hello")    # a comment can also go after code
```

Output:

```text
hello
```

**2. `len()` gives the length.** `len` returns the total number of items in a container, such as the number of characters in a string or the number of items in a list.

```python
print(len("Jimhalpertt"))
print(len(["joey", "ruchik", "kota"]))
```

Output:

```text
11
3
```

**3. `range()` has three parameters:** the lower limit, the upper limit and the step size, written `range(lower limit, upper limit, step size)`. The full explanation, with examples, is under **range()** in the `for` loops part above.

## Day 1 – In my own words (what I understood)

- **Python** is a programming language, a way of giving instructions to a computer. I can run it in Jupyter Notebook, Anaconda or VS Code.
- **`print()`** shows something on the screen.
- A **variable** holds a value, and it always holds the *current* value. If I assign a new one, the old one is gone.
- **Data types:** int (whole numbers), float (decimals), str (anything in quotes), bool (`True`/`False`) and complex (I can ignore it for now). Python works out the type by itself (dynamic typing).
- **Casting** changes one type into another. Python sometimes does it by itself (implicit) and sometimes I ask for it (explicit, like `int('5')`).
- **Naming rules:** a name can't start with a number or a special character, and I shouldn't reuse built-in names like `str`. If I want a name like that, I put an underscore in front (`_str`).
- **Operators:** `+ - * /` as usual, `%` gives the remainder, `**` is the power (square, cube) and `//` is floor division (the divide result rounded down). Comparison operators give `True` or `False`. `and`, `or`, `not` combine conditions. `+=` and `-=` update a variable in one step.
- **`input()`** asks the user to type something. It always comes back as a string. **f-strings** and **`.format()`** put values inside text.
- **`if` / `elif` / `else`** make the program choose a path. They can be nested.
- **Loops** repeat things: `for` when I know how many times (or I have a collection to go through), `while` when I don't know how many times. `range(start, stop, step)` gives the numbers, and the stop is not included (add `+1` to include it). `break` leaves the loop. `continue` skips the rest of this round and goes to the next one.

## Day 1 – Extras from the notebook

*These topics are in the Session 1 notebook but weren't part of your own notes yet, so they are kept here at the end.*

### Boolean expressions and `is` vs `==`

The boolean operators `and`, `or` and `not` are covered with examples and a truth table under **Operators** above (Logical). This section is about `is` versus `==`.

`==` asks whether two values are **equal**. `is` asks whether two names point at the **exact same object** in memory.

```python
print('a' == 'a')
print('a' is 'a')   # True here, but Python warns you (SyntaxWarning)

x = [1, 2]
y = [1, 2]
print(x == y)       # same values
print(x is y)       # two separate objects
```

Output:

```text
True
True
True
False
```

Use `==` to compare values, such as strings and numbers. Save `is` for things like `x is None`.

### The 5 collection types (preview)

Python has five main ways to hold many values together. Each one gets its own session later:

1. **Strings**: text, a sequence of characters
2. **Lists**: ordered and changeable
3. **Tuples**: ordered and fixed
4. **Sets**: unordered and unique
5. **Dictionaries (dict)**: key-value pairs

### Common mistakes from the notebook

- **Mixing a string and a number.** `"text" + 7` raises a `TypeError`. Use `str(7)`, or an f-string.
- **Unescaped quote inside a string.** `'ruchik's kota'` raises a `SyntaxError`. Use double quotes outside, or escape with `\`.
- **Off-by-one with `range`.** `range(len(x) + 1)` runs one step too many. In the notebook it counts 0 to 11 and gives 66, which matches the list total only because the list happens to be 1 to 11. If you index with it (`x[i]`), the last pass fails with an `IndexError`. The right form is `range(len(x))`.
- **`input()` returns a string.** Convert with `int()` or `float()` before doing maths with it.
- **`.format()` with the same index twice.** `"{0} ... {0}".format(a, b)` prints `a` both times. Use `{0}` and `{1}` for two different values.
- **Using `is` to compare values.** Use `==` instead.
- **Forgetting to update a `while` loop's counter.** The loop then never ends.

What each mistake looks like when you run it:

```python
print("text" + 7)
```

Output:

```text
TypeError: can only concatenate str (not "int") to str
```

```python
print('ruchik's kota')
```

Output:

```text
SyntaxError: unterminated string literal (detected at line 1)
```

```python
x = [10, 20, 30]
for i in range(len(x) + 1):
    print(x[i])
```

Output:

```text
10
20
30
IndexError: list index out of range
```

```python
print("{0} and {0}".format("a", "b"))
```

Output:

```text
a and a
```
