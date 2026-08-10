# Python Implementations

## 1. Python Is a Specification, Not an Implementation

Python defines language behavior.

An implementation provides the machinery that executes that language.

Therefore:

[
\text{Python} \neq \text{CPython}
]

CPython is simply the dominant implementation.

---

# 2. Major Python Implementations

## CPython

The reference implementation.

Written primarily in:

```text
C
```

Architecture:

```text
Python source
     ↓
CPython compiler
     ↓
code object
     ↓
bytecode
     ↓
CPython runtime
```

Most Python users are using CPython unless explicitly using another implementation.

---

## PyPy

PyPy uses a tracing JIT architecture.

Conceptually:

```text
Python source
     ↓
PyPy runtime
     ↓
interpreter
     ↓
hot code detection
     ↓
JIT compilation
     ↓
native machine code
```

Its major motivation is improving execution speed for suitable workloads.

---

## Jython

Python implemented on the JVM.

```text
Python
  ↓
Jython
  ↓
JVM
  ↓
Java ecosystem
```

Useful when integrating Python semantics with JVM infrastructure.

---

## IronPython

Python implementation targeting the .NET ecosystem.

```text
Python
  ↓
IronPython
  ↓
.NET runtime
```

---

## GraalPy

Python implementation built within the GraalVM ecosystem.

Its architecture allows Python programs to interact with GraalVM's runtime and optimization infrastructure.

---

# 3. Why Multiple Implementations Exist

Different implementations optimize different constraints.

| Implementation | Runtime     | Main Strength           |
| -------------- | ----------- | ----------------------- |
| CPython        | Native      | Compatibility/ecosystem |
| PyPy           | RPython/JIT | JIT optimization        |
| Jython         | JVM         | Java integration        |
| IronPython     | .NET        | .NET integration        |
| GraalPy        | GraalVM     | Polyglot/JIT ecosystem  |

Therefore:

[
\text{Python semantics}
]

is the common abstraction while:

[
\text{runtime architecture}
]

can differ substantially.

---

# 4. Why CPython Dominates

CPython has an enormous ecosystem.

Many packages depend directly or indirectly on:

* CPython C APIs
* native extensions
* CPython-specific behavior
* established packaging infrastructure

Therefore compatibility is not merely:

```text
"Does this implementation understand Python syntax?"
```

It can also be:

```text
"Can this implementation run the entire ecosystem?"
```

This is a much harder problem.

---

# 5. Python Compatibility

A Python program can rely on different layers.

```text
Layer 1
Language semantics

Layer 2
Standard library

Layer 3
Implementation behavior

Layer 4
Implementation-specific APIs

Layer 5
Native extension ecosystem
```

Portable Python should ideally depend primarily on the upper layers.

---

# 6. CPython Extensions

CPython allows native code to interact directly with Python objects.

Historically this happens through the CPython C API.

Conceptually:

```text
Python
   │
   ▼
Python object
   │
   ▼
C extension
   │
   ▼
native machine code
```

This is one reason Python can combine:

[
\text{high-level ergonomics}
]

with:

[
\text{native execution performance}
]

---

# 7. Implementation-Specific Code

Some code explicitly depends on CPython.

For example:

```python
import sys

print(sys.implementation.name)
```

On CPython:

```text
cpython
```

You can also inspect:

```python
sys.implementation
```

This is useful when debugging runtime-specific behavior.

---

# 8. Engineering Principle

When writing libraries:

> Prefer language-level guarantees unless implementation-specific behavior is deliberately required.

When writing performance-sensitive infrastructure:

> Know exactly which implementation your assumptions target.

This distinction becomes extremely important later when studying:

* reference counting
* garbage collection
* GIL
* memory allocation
* bytecode
* C extensions
* free-threaded CPython
