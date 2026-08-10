Control Flow
1. Conditional Execution
if condition:
    ...
elif other_condition:
    ...
else:
    ...

The condition is evaluated according to Python's truth-value protocol.

2. Loops

Python provides:

for
while

A for loop is fundamentally iteration over an iterable.

for x in iterable:
    ...

Conceptually:

iterator = iter(iterable)

while True:
    try:
        x = next(iterator)
    except StopIteration:
        break

    ...

This model becomes extremely important later.

3. Break
for x in items:
    if x == target:
        break

Terminates the loop.

4. Continue
for x in items:
    if x < 0:
        continue

    process(x)

Skips to the next iteration.

5. Else on Loops

Python allows:

for x in items:
    if found(x):
        break
else:
    print("not found")

The else executes when the loop terminates normally rather than through break.

6. While Else
while condition:
    ...
else:
    ...

Same principle.

7. Exceptions Affect Control Flow

Exceptions can interrupt normal control flow:

try:
    result = risky()
except ValueError:
    recover()

Exceptions are therefore another control-flow mechanism.

Brain-Twisting Questions 🧠
Q1

What does this print?

for i in range(5):
    if i == 3:
        break
else:
    print("completed")

print("done")

Why doesn't "completed" appear?

Q2

Explain this:

for i in range(5):
    if i == 3:
        break
else:
    print("not found")

How would you express the same semantics using a flag?

Why is the Python version often cleaner?

Q3

What exactly is a for loop doing when the object is a custom class?

Implement the minimal protocol required to make:

for x in obj:
    print(x)

work.