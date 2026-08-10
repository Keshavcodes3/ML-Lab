Lists
1. Lists Are Mutable Sequences
items = [1, 2, 3]

They support:

indexing
slicing
mutation
insertion
deletion
iteration
2. Mutation
items.append(4)

changes the existing list.

Unlike strings:

items[0] = 100

is legal.

3. Dynamic Array Model

A CPython list behaves conceptually like a dynamic array.

list object
┌───────────────┐
│ size          │
│ capacity      │
│ pointer ──────┼──► object
│ pointer ──────┼──► object
│ pointer ──────┼──► object
└───────────────┘

The list stores references to objects rather than embedding arbitrary Python objects directly.

4. Complexity

Typical complexity:

Operation	Complexity
a[i]	O(1)
append	amortized O(1)
pop()	O(1)
insert beginning	O(n)
delete beginning	O(n)
search	O(n)
5. List Aliasing
a = [1, 2]
b = a

b.append(3)

print(a)

Mutation is visible through both names.

6. Shallow Copy
a = [[1], [2]]
b = a.copy()

The outer list is copied.

The inner lists are not.

a ──► outer ──► inner1
              └► inner2

b ──► outer' ─► inner1
               └► inner2
7. List Comprehension
squares = [x * x for x in range(10)]

Conceptually:

squares = []

for x in range(10):
    squares.append(x * x)
Brain-Twisting Questions 🧠
Q1

Predict:

x = [[]] * 5

x[0].append(1)

print(x)

Why does one mutation appear everywhere?

Q2

Why is:

a = [[0] * 3] * 3

dangerous?

How would you construct a true 3×3 independent matrix?

Q3

What happens internally when a list repeatedly grows?

Why can append() be amortized (O(1)) even though resizing sometimes costs (O(n))?