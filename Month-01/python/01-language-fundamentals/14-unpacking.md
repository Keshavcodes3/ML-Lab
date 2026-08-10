Unpacking
1. Basic Unpacking
point = (10, 20)

x, y = point

Conceptually:

iter(point)
    ↓
10 → x
20 → y

Unpacking works with iterables, not only tuples.

2. List Unpacking
x, y, z = [1, 2, 3]
3. String Unpacking
a, b, c = "ABC"

produces:

a = "A"
b = "B"
c = "C"
4. Extended Unpacking
first, *middle, last = [1, 2, 3, 4, 5]

Result:

first = 1
middle = [2, 3, 4]
last = 5

The starred target absorbs the remaining values.

5. Starred Unpacking
a, *rest = range(5)

gives:

a = 0
rest = [1, 2, 3, 4]

The starred result is a list.

6. Function Arguments
args = [1, 2, 3]

foo(*args)

expands the iterable into positional arguments.

Dictionary unpacking:

config = {
    "host": "localhost",
    "port": 8000,
}

connect(**config)

expands mappings into keyword arguments.

7. Dictionary Merging

Python supports:

merged = {
    **defaults,
    **user_config,
}

If duplicate keys occur, later values override earlier ones.

8. Multiple Assignment
a, b = b, a

This is one of Python's elegant features.

Conceptually, the right-hand side is evaluated before bindings are updated.

This allows:

a, b = b, a

without a temporary variable.

9. Unpacking Is Protocol-Based

The important insight:

a, b = obj

requires iteration semantics.

It is not fundamentally:

"tuple destructuring."

It is iterable unpacking.

Brain-Twisting Questions 🧠
Q1

Predict:

a, *b, c = range(10)

print(a)
print(b)
print(c)

What type is b?

Q2

What happens?

a, b = [1, 2, 3]

Why can't Python simply ignore the extra element?

What invariant does unpacking enforce?

Q3

Implement an object that supports:

a, b, c = obj

without making obj a list or tuple.

What protocol must it implement?

Q4 🔥

What does this do?

def f():
    yield 1
    yield 2
    yield 3

a, *b = f()

print(a)
print(b)

Explain the entire chain:

generator
   ↓
iterator protocol
   ↓
unpacking
   ↓
starred target
   ↓
list construction

Don't just give the output. Derive it.