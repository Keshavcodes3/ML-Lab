# Interpreter vs Compiler

## 1. The False Dichotomy

A common statement is:

> "Compiled languages are fast; interpreted languages are slow."

This is too simplistic.

Modern language runtimes often combine:

* parsing
* compilation
* intermediate representations
* interpretation
* JIT compilation
* native execution

Python is no exception.

---

# 2. CPython Execution Pipeline

A simplified CPython pipeline is:

```text
.py source
    ↓
Tokenizer
    ↓
Parser
    ↓
AST
    ↓
Compiler
    ↓
Code Object
    ↓
Bytecode
    ↓
CPython Runtime
    ↓
Machine instructions
```

The source file is therefore not directly executed character-by-character.

---

# 3. Tokenization

Source:

```python
x = a + b
```

is transformed into lexical units roughly corresponding to:

```text
NAME(x)
=
NAME(a)
+
NAME(b)
```

The tokenizer converts raw source text into tokens.

---

# 4. Parsing

Tokens are organized according to Python's grammar.

Conceptually:

```text
assignment
 ├── target: x
 └── expression
      ├── a
      ├── +
      └── b
```

The result is represented by an Abstract Syntax Tree.

You can inspect an AST:

```python
import ast

tree = ast.parse("x = a + b")

print(ast.dump(tree, indent=2))
```

---

# 5. Compilation

The AST is compiled into a code object.

A function:

```python
def add(a, b):
    return a + b
```

has a code object containing information such as:

* bytecode
* constants
* local variable metadata
* names
* source metadata

You can inspect:

```python
add.__code__
```

---

# 6. Bytecode

CPython executes an intermediate instruction representation.

Inspect it:

```python
import dis

def add(a, b):
    return a + b

dis.dis(add)
```

The exact instructions depend on the Python version.

Conceptually:

```text
load a
load b
perform addition
return result
```

Bytecode is an implementation detail of CPython and can change between versions.

---

# 7. Interpretation

The runtime executes bytecode through CPython's execution machinery.

Conceptually:

```text
bytecode instruction
        ↓
dispatch
        ↓
execute operation
        ↓
next instruction
```

This execution layer introduces overhead compared with executing optimized native machine code directly.

---

# 8. JIT Compilation

A JIT changes the picture.

Instead of repeatedly interpreting the same code:

```text
bytecode
 ↓
interpreter
 ↓
bytecode
 ↓
interpreter
 ↓
bytecode
 ↓
interpreter
```

a JIT can potentially produce:

```text
bytecode
 ↓
observe hot path
 ↓
compile
 ↓
native code
 ↓
execute repeatedly
```

---

# 9. Compilation Exists on a Spectrum

Think of execution strategies as:

```text
Source
  │
  ├── Direct interpretation
  │
  ├── Bytecode interpretation
  │
  ├── AOT compilation
  │
  └── JIT compilation
```

Real runtimes frequently combine multiple techniques.

---

# 10. Why This Matters

Understanding the execution pipeline explains:

### Startup cost

Parsing and compilation happen before useful execution.

### Dynamic dispatch

Runtime type information may need to be consulted.

### Bytecode overhead

Python operations often involve runtime machinery.

### Profiling

You need to identify whether time is spent in:

```text
Python runtime
native code
system calls
I/O
allocation
synchronization
```

### Optimization

You cannot optimize effectively without understanding where execution actually occurs.

---

# 11. The Correct Mental Model

Do not think:

```text
Python = interpreted
```

Think:

```text
Python language
       ↓
implementation
       ↓
compiler
       ↓
intermediate representation
       ↓
runtime
       ↓
optional native/JIT mechanisms
```

The language defines semantics.

The implementation determines execution strategy.
