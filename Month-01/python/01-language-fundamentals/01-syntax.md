# Python Syntax

## 1. Syntax Is the Surface Grammar

Python syntax defines how source text is structured.

At a high level:

```text
source code
    ↓
tokens
    ↓
grammar
    ↓
AST
    ↓
executable representation
```

Syntax answers:

> "Is this program structurally valid?"

Semantics answers:

> "What does this valid program mean?"

These are different questions.

---

# 2. Statements vs Expressions

An expression produces a value.

```python
10 + 20
```

```python
user.name
```

```python
foo()
```

A statement performs an action or controls execution.

```python
x = 10

if x > 5:
    print(x)
```

Some constructs combine expression and statement-like behavior.

For example:

```python
x = 10
```

is an assignment statement.

---

# 3. Indentation Is Syntax

Python uses indentation to define blocks.

```python
if True:
    print("inside")
    print("still inside")

print("outside")
```

Conceptually:

```text
if
├── print
└── print

print
```

Indentation is therefore not merely formatting.

This is invalid:

```python
if True:
print("hello")
```

---

# 4. Multiple Statements

Python permits semicolon-separated statements:

```python
x = 10; y = 20
```

but this is generally less readable than:

```python
x = 10
y = 20
```

The language allows it, but engineering style may discourage it.

---

# 5. Line Continuation

Parentheses automatically permit multiline expressions:

```python
result = (
    first_value
    + second_value
    + third_value
)
```

Lists:

```python
items = [
    1,
    2,
    3,
]
```

Dictionaries:

```python
config = {
    "host": "localhost",
    "port": 8000,
}
```

---

# 6. Explicit Continuation

A backslash can continue a line:

```python
result = 10 + \
         20 + \
         30
```

Usually prefer implicit continuation through parentheses.

---

# 7. Comments

```python
# This is a comment
x = 10  # inline comment
```

Comments are ignored by the Python runtime after tokenization.

But comments can still matter to tooling, linters, documentation generators, and humans.

---

# 8. Identifiers

Valid:

```python
user
user_id
_private
value2
```

Invalid:

```python
2value
user-id
class
```

Python identifiers are Unicode-aware.

For example:

```python
π = 3.14159
```

is syntactically legal.

Engineering wisdom, however, strongly favors conventional ASCII identifiers.

---

# 9. Keywords

Python reserves certain words:

```python
if
else
for
while
def
class
return
yield
async
await
match
case
```

You can inspect them:

```python
import keyword

print(keyword.kwlist)
```

---

# 10. Assignment Is Not Equality

```python
x = 10
```

means binding.

While:

```python
x == 10
```

means equality comparison.

This distinction becomes foundational later.

---

# 11. Parsing the Program

Try:

```python
import ast

source = """
x = 10
y = x + 20
"""

tree = ast.parse(source)

print(ast.dump(tree, indent=2))
```

The parser transforms syntax into structured representation.

---

# Brain-Twisting Questions 🧠

### Q1

What does this print?

```python
x = 10

if x:
    print("A")
else:
    print("B")
```

Easy.

Now:

```python
if x := 0:
    print("A")
else:
    print("B")
```

What is the difference between assignment and expression semantics here?

---

### Q2

Why is this valid?

```python
x = (
    1 +
    2 +
    3
)
```

while this isn't?

```python
x = 1 +
    2
```

What does the parser know from the parentheses?

---

### Q3

Predict:

```python
x = [
    1,
    2,
    3,
]

print(x)
```

Why is the trailing comma legal?

What does the grammar gain from allowing it?
