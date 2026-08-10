Tuples
1. Immutable Sequences
point = (10, 20)

Tuples cannot have their element references reassigned.

point[0] = 100

is invalid.

2. Tuple Packing
x = 1, 2, 3

is equivalent to:

x = (1, 2, 3)

The parentheses are not what create the tuple.

The comma is fundamental.

3. Singleton Tuple

This:

x = (42,)

is a tuple.

This:

x = (42)

is an integer.

4. Unpacking
x, y = (10, 20)

Python destructures the iterable.

5. Tuples Can Contain Mutable Objects

"Tuples are immutable" does not mean recursively immutable.

x = ([1, 2], 3)

x[0].append(4)

is legal.

The tuple's reference to the list didn't change.

The list itself mutated.

6. Hashability

A tuple can be hashable if its elements are hashable.

x = (1, 2, 3)

d = {x: "value"}

But:

x = ([1], 2)

cannot be used as a dictionary key because the list is unhashable.

Brain-Twisting Questions 🧠
Q1

Why is this legal?

x = ([1, 2], 3)
x[0].append(4)

If tuples are immutable, what exactly is immutable?

Q2

Predict:

a = (1, 2)
b = (1, 2)

print(a == b)
print(a is b)

Why can implementation optimizations make is behavior surprising?

Q3

Why can:

(1, 2, 3)

be a dictionary key but:

([1, 2], 3)

cannot?

Define hashability formally.