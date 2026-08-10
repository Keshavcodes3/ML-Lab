# What Is Python?

## 1. Python Is a Language Specification

Python is not synonymous with CPython.

Python defines a language and its semantics:

* syntax
* expressions
* statements
* objects
* types
* functions
* exceptions
* modules
* protocols
* execution semantics

Different implementations can execute Python programs.

The major distinction is:

```text
Python
  │
  ├── Language specification
  │
  └── Implementations
       ├── CPython
       ├── PyPy
       ├── GraalPy
       ├── Jython
       └── IronPython
```

The implementation determines **how** Python semantics are realized.

---

# 2. Python Is Dynamically Typed

Consider:

```python
x = 10
x = "hello"
x = [1, 2, 3]
```

The name `x` can successively refer to objects of different types.

The important model is:

```text
name ───────► object
```

not:

```text
variable ───► fixed memory slot
```

Every object has:

```text
identity
type
value/state
```

Conceptually:

[
O = (id, type, state)
]

Python's type system determines which operations are valid for an object.

---

# 3. Everything Is an Object

In Python:

```python
x = 42
```

`42` is an object.

But so are:

```python
"hello"
[1, 2, 3]
{"x": 10}
```

and even:

```python
def add(a, b):
    return a + b
```

The function itself is an object.

Classes are objects.

Modules are objects.

Types are objects.

This object-centric model explains much of Python's flexibility.

---

# 4. Names Bind to Objects

Consider:

```python
a = [1, 2, 3]
b = a
```

The assignment does not copy the list.

Instead:

```text
a ─────┐
       │
       ▼
   [1, 2, 3]
       ▲
       │
b ─────┘
```

Therefore:

```python
a is b
```

is `True`.

This distinction between:

* identity
* equality
* binding
* mutation
* rebinding

is foundational Python knowledge.

---

# 5. Python Is Protocol-Oriented

Python frequently determines behavior through protocols rather than explicit inheritance.

For example:

```python
for item in obj:
    ...
```

requires `obj` to support iteration.

Python does not necessarily care whether `obj` is a:

```text
list
tuple
set
generator
custom object
file
```

It cares whether the appropriate protocol exists.

Python's data model exposes these protocols through special methods:

```python
__iter__
__next__
__getitem__
__len__
__call__
__enter__
__exit__
__eq__
__add__
```

This is the foundation of Python's duck-typing model.

---

# 6. Python Is Multi-Paradigm

Python supports several programming styles.

### Imperative

```python
total = 0

for x in numbers:
    total += x
```

### Functional

```python
squares = list(map(lambda x: x * x, numbers))
```

### Object-oriented

```python
class User:
    ...
```

### Procedural

```python
def process_data(data):
    ...
```

### Concurrent

```python
await asyncio.gather(...)
```

Python does not force a single paradigm.

---

# 7. Python's Runtime

A Python program eventually has to execute machine instructions.

A simplified CPython path is:

```text
Python source
     │
     ▼
Tokenization
     │
     ▼
Parsing
     │
     ▼
AST
     │
     ▼
Code object
     │
     ▼
Bytecode
     │
     ▼
CPython interpreter
     │
     ▼
Machine instructions
```

This is simplified but gives the correct architectural direction.

---

# 8. Python Is Not Simply "Interpreted"

The common statement:

> Python is an interpreted language.

is incomplete.

CPython compiles source into an intermediate representation, traditionally called bytecode, and then executes that representation through its runtime machinery.

You can inspect bytecode:

```python
import dis

def add(a, b):
    return a + b

dis.dis(add)
```

Therefore:

```text
source
  ↓
compiler
  ↓
code object
  ↓
bytecode
  ↓
interpreter/runtime
```

The distinction between compiled and interpreted execution is therefore more nuanced than a binary classification.

---

# 9. Python's Strength

Python's primary strength is not raw execution speed.

Its strength comes from the combination of:

```text
high-level abstractions
+
dynamic object model
+
rich standard library
+
extensive ecosystem
+
native-code integration
+
excellent developer productivity
```

Python can orchestrate extremely high-performance native systems.

For example:

```text
Python
  ↓
C / C++
  ↓
SIMD / native CPU
  ↓
GPU / accelerator
```

This distinction becomes important when analyzing Python performance.

---

# 10. Python's Weaknesses

Python has real costs.

Important ones include:

* object overhead
* dynamic dispatch
* interpreter overhead
* memory consumption
* serialization overhead
* startup costs
* GIL constraints in traditional CPython builds
* weaker guarantees than statically typed languages
* runtime errors that static languages may catch earlier

Good Python engineering is therefore about understanding where the abstraction boundaries become expensive.

---

# 11. Python's Major Execution Models

Python supports several mechanisms for concurrent execution.

### Sequential

```text
A → B → C → D
```

### Threading

```text
Thread A ────────►
Thread B ─────────────►
```

### Multiprocessing

```text
Process A ─────────►
Process B ─────────►
Process C ─────────►
```

### AsyncIO

```text
Task A ──await──┐
Task B ────────┐│
Task C ──await─┘│
                ▼
            Event Loop
```

These models solve different problems.

Understanding their mechanics is a major part of this handbook.

---

# 12. Python's Design Philosophy

Python strongly emphasizes readability and explicitness.

The famous guiding principles can be inspected through:

```python
import this
```

The philosophy includes ideas such as:

```text
explicit > implicit
readability > cleverness
simple > complex
complex > complicated
```

These are not merely aesthetic preferences.

They influence:

* API design
* standard-library design
* error handling
* language evolution
* community conventions

---

# 13. The Goal of This Handbook

The goal is not:

> Learn Python syntax.

The goal is:

[
\boxed{
\text{Understand Python as a language, runtime, and engineering system}
}
]

We will progress through:

```text
Syntax
  ↓
Semantics
  ↓
Object Model
  ↓
Data Model
  ↓
Runtime
  ↓
Memory
  ↓
Concurrency
  ↓
Parallelism
  ↓
Async
  ↓
Performance
  ↓
CPython Internals
```

By the end, Python should no longer feel like a collection of syntax rules.

It should feel like a system whose behavior can be derived.
