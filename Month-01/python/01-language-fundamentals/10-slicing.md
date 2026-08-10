Slicing
1. General Form

Python slicing follows:

sequence[start:stop:step]

where:

start is inclusive
stop is exclusive
step controls traversal
2. Basic Slicing
x = [0, 1, 2, 3, 4]

x[1:4]

returns:

[1, 2, 3]
3. Negative Indices
x[-1]

means the last element.

x[-3:]

returns the last three elements.

4. Step
x[::2]

takes every second element.

x[::-1]

reverses the sequence.

5. Slice Objects

Slices are objects.

s = slice(1, 5, 2)

x[s]

This is useful when constructing generic indexing logic.

6. Slice Assignment

For mutable sequences:

x = [1, 2, 3, 4]

x[1:3] = [20, 30, 40]

The replacement does not need to have the same length.

Result:

[1, 20, 30, 40, 4]
7. Slice Deletion
del x[1:3]

removes that range.

Brain-Twisting Questions 🧠
Q1

Predict:

x = [0, 1, 2, 3, 4, 5]

print(x[5:1:-2])

Derive the indices manually.

Q2

What does this do?

x = [1, 2, 3, 4, 5]

x[1:4] = [9]

print(x)

Why is the resulting length different?

Q3

Why does:

x[::-1]

usually create a new sequence instead of creating a lazy reversed view?

What are the memory implications?