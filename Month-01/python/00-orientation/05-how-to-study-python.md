# How to Study Python

## 1. Objective

The objective of this handbook is not merely to become productive with Python.

The objective is:

[
\boxed{
\text{Predict Python behavior from first principles}
}
]

That requires studying Python at multiple abstraction levels.

---

# 2. The Five Layers

Every major topic should eventually be understood through five layers.

```text
Layer 1 — Syntax
        ↓
Layer 2 — Semantics
        ↓
Layer 3 — Runtime
        ↓
Layer 4 — Implementation
        ↓
Layer 5 — Engineering consequences
```

Example:

```python
x = [1, 2, 3]
```

### Syntax

Assignment syntax.

### Semantics

The name `x` becomes bound to a list object.

### Runtime

A namespace entry points to an object.

### Implementation

CPython represents the list using internal runtime structures and references.

### Engineering consequence

Aliasing and mutation can affect other references to the same object.

---

# 3. Never Learn a Feature in Isolation

Suppose you're learning:

```python
asyncio.Lock
```

Do not stop at:

```python
lock = asyncio.Lock()

async with lock:
    ...
```

Eventually ask:

```text
What is a coroutine?
        ↓
What is await?
        ↓
What is an awaitable?
        ↓
What is a Task?
        ↓
What is the event loop?
        ↓
How is scheduling performed?
        ↓
Where does suspension happen?
        ↓
How does cancellation propagate?
        ↓
What happens when code blocks the event loop?
```

This approach produces durable understanding.

---

# 4. Use Experiments

Python is unusually introspectable.

Exploit that.

### Object identity

```python
x = []
y = x

print(id(x))
print(id(y))
print(x is y)
```

### Type

```python
print(type(x))
print(isinstance(x, list))
```

### Reference count

```python
import sys

x = []

print(sys.getrefcount(x))
```

### Bytecode

```python
import dis

def add(a, b):
    return a + b

dis.dis(add)
```

### AST

```python
import ast

tree = ast.parse("x = a + b")

print(ast.dump(tree, indent=2))
```

### Runtime implementation

```python
import sys

print(sys.implementation)
```

Experiments turn abstract claims into observable behavior.

---

# 5. Read the Documentation

For important concepts, use three sources of truth:

```text
Language reference
        +
Standard library documentation
        +
Implementation documentation/source
```

These answer different questions.

### Language reference

> What behavior does Python define?

### Standard library

> How is this API intended to behave?

### CPython source

> How does this implementation realize it?

Never confuse the third with the first.

---

# 6. Read Source Strategically

You do not need to read the entire CPython repository.

Instead, follow behavior.

Suppose you want to understand:

```python
a + b
```

Start from:

```text
Python expression
    ↓
data model
    ↓
__add__
    ↓
CPython implementation
```

Likewise:

```python
for x in obj:
```

follow:

```text
iteration syntax
    ↓
iter(obj)
    ↓
__iter__
    ↓
iterator
    ↓
__next__
```

Study the execution path rather than randomly reading source code.

---

# 7. Derive Before Memorizing

Suppose:

```python
a = [1, 2]
b = a

b.append(3)
```

Don't memorize:

> Lists are mutable.

Derive it:

```text
a ─────┐
       ↓
     list object
       ↑
b ─────┘

append()
   ↓
mutates object
   ↓
both names observe new state
```

The derivation is more valuable than the fact.

---

# 8. Benchmark Claims

Never assume:

> This is faster.

Measure it.

Use:

```python
import timeit

timeit.timeit(...)
```

For more serious work:

```text
benchmark
   ↓
profile
   ↓
identify bottleneck
   ↓
form hypothesis
   ↓
optimize
   ↓
benchmark again
```

Optimization without measurement is speculation.

---

# 9. Study Concurrency Experimentally

Concurrency concepts should be demonstrated with actual timing and synchronization behavior.

For example:

```text
sequential
    ↓
threading
    ↓
multiprocessing
    ↓
asyncio
```

Compare:

[
T_{sequential}
]

against:

[
T_{concurrent}
]

and understand *why* the difference exists.

Then investigate:

* scheduling
* contention
* context switching
* synchronization
* queueing
* cancellation
* backpressure

---

# 10. Build Small Runtime Experiments

Every difficult concept should have a minimal reproducible program.

Examples:

```text
experiments/
├── identity.py
├── mutation.py
├── closures.py
├── descriptors.py
├── gc.py
├── bytecode.py
├── threading.py
├── race_condition.py
├── deadlock.py
├── multiprocessing.py
├── asyncio.py
└── cancellation.py
```

A 30-line experiment often teaches more than 30 pages of prose.

---

# 11. Maintain a Complexity Model

For important operations, track:

[
T(n)
]

and:

[
S(n)
]

where:

* (T(n)) = time complexity
* (S(n)) = space complexity

For example:

```text
list indexing       O(1)
list append         amortized O(1)
list search         O(n)
dict lookup         average O(1)
set membership      average O(1)
sorting             O(n log n)
```

But don't stop at Big-O.

Also understand:

```text
constant factors
memory locality
allocation
cache behavior
branching
object overhead
```

---

# 12. Learn Failure Modes

Every abstraction should be studied together with how it fails.

Examples:

### Mutable defaults

```python
def f(items=[]):
    ...
```

### Late binding

```python
funcs = [
    lambda: i
    for i in range(3)
]
```

### Circular imports

```text
A → B → A
```

### Deadlocks

```text
Thread A
  lock 1
  waits for lock 2

Thread B
  lock 2
  waits for lock 1
```

### Event-loop blocking

```python
async def handler():
    time.sleep(10)
```

These aren't trivia questions.

They represent violations of useful mental models.

---

# 13. Build From First Principles

The recommended progression is:

```text
Language
   ↓
Objects
   ↓
Functions
   ↓
Protocols
   ↓
Abstractions
   ↓
OOP
   ↓
Memory
   ↓
Runtime
   ↓
Concurrency
   ↓
Parallelism
   ↓
Async
   ↓
Performance
   ↓
Internals
```

Do not jump randomly between topics.

Later concepts should rest on earlier ones.

---

# 14. The Mastery Test

You haven't mastered a topic because you can write code using it.

You've mastered it when you can answer:

### Semantics

> What does Python guarantee?

### Mechanics

> What happens during execution?

### Implementation

> How does CPython implement it?

### Memory

> What objects and allocations are involved?

### Complexity

> What are the computational costs?

### Concurrency

> What happens when multiple execution contexts interact with it?

### Failure

> How can this abstraction break?

### Design

> When should I use it and when should I avoid it?

---

# 15. The Final Standard

For every major topic in this handbook, aim for this progression:

```text
I can use it
      ↓
I understand it
      ↓
I can explain it
      ↓
I can predict its behavior
      ↓
I can debug it
      ↓
I can benchmark it
      ↓
I understand its implementation
      ↓
I can design systems around it
```

The final destination is not:

> "I know Python."

It is:

[
\boxed{
\text{I understand enough of Python's semantics and runtime to reason about its behavior.}
}
]

That is the standard this handbook should maintain.
