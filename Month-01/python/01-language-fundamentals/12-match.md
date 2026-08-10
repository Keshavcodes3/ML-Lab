Structural Pattern Matching

Python's match statement provides structural pattern matching.

match value:
    case pattern:
        ...

It is more powerful than a traditional switch statement.

1. Literal Matching
status = 200

match status:
    case 200:
        print("OK")
    case 404:
        print("Not Found")
2. OR Patterns
match status:
    case 400 | 401 | 403:
        print("client error")
3. Binding
match point:
    case (x, y):
        print(x, y)

The pattern doesn't merely compare.

It can destructure and bind.

4. Sequence Patterns
match values:
    case [first, second]:
        ...
5. Mapping Patterns
match user:
    case {"name": name, "age": age}:
        print(name, age)
6. Guards
match value:
    case int(x) if x > 0:
        print("positive")

Pattern matching and boolean conditions can work together.

7. Class Patterns

Classes can participate in pattern matching.

class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

Then:

match point:
    case Point(x, y):
        print(x, y)
Brain-Twisting Questions 🧠
Q1

What is the difference between:

case x:

and:

case 10:

Why does the first one potentially match almost anything?

Q2

What happens?

value = [1, 2]

match value:
    case [x, y]:
        print(x + y)

Where did x and y come from?

Are they comparisons or bindings?

Q3

Design a pattern that matches:

HTTP response
where status is 2xx
and payload contains "data"

without writing a traditional if chain.