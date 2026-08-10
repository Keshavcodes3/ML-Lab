# CPython vs PyPy

## 1. The Fundamental Difference

The important distinction is runtime architecture.

### CPython

```text
Python source
      ↓
compiler
      ↓
bytecode
      ↓
CPython interpreter
      ↓
native execution
```

### PyPy

```text
Python source
      ↓
PyPy runtime
      ↓
interpreter
      ↓
JIT
      ↓
optimized machine code
```

The major conceptual difference is:

[
\boxed{\text{CPython: interpreter-centric}}
]

versus:

[
\boxed{\text{PyPy: JIT-centric}}
]

---

# 2. What Is a JIT?

JIT means:

> Just-In-Time compilation.

Instead of compiling everything ahead of execution, a JIT can observe runtime behavior and compile frequently executed paths.

Conceptually:

```text
Program
  ↓
Interpreter
  ↓
Observe execution
  ↓
Identify hot path
  ↓
Optimize
  ↓
Compile
  ↓
Native machine code
```

Suppose:

```python
for i in range(10_000_000):
    total += i
```

A JIT can potentially identify the repeated loop as hot code and optimize it.

---

# 3. Why CPython Doesn't Simply JIT Everything

CPython prioritizes:

* compatibility
* predictable semantics
* ecosystem stability
* implementation simplicity
* native extension compatibility

A JIT introduces additional complexity.

The runtime must reason about:

```text
types
guards
deoptimization
code generation
runtime assumptions
```

---

# 4. PyPy's Advantage

PyPy can perform extremely well on workloads with:

* long-running loops
* Python-level computation
* predictable execution paths
* limited interaction with unsupported native extensions

The JIT can exploit runtime information unavailable to a purely interpreter-driven execution model.

---

# 5. CPython's Advantage

CPython generally wins in ecosystem compatibility.

Especially important:

```text
Python
 ↓
C extensions
 ↓
native libraries
```

A huge amount of Python infrastructure assumes CPython.

---

# 6. Native Extensions Complicate the Picture

Suppose Python calls native code:

```text
Python
  ↓
extension
  ↓
C/C++
  ↓
native execution
```

The performance difference between interpreters may become much less important because the expensive computation isn't occurring in Python bytecode.

This is why:

> "PyPy is faster than CPython"

is an incomplete statement.

Performance depends on the workload.

---

# 7. Benchmarking Principle

Never choose a runtime based solely on theoretical architecture.

Measure:

[
T_{total}
=========

T_{startup}
+
T_{Python}
+
T_{native}
+
T_{IO}
+
T_{serialization}
]

A JIT may reduce:

[
T_{Python}
]

while having little effect on:

[
T_{IO}
]

or:

[
T_{native}
]

---

# 8. Practical Decision Model

Use CPython when:

* ecosystem compatibility matters
* native extensions are important
* predictable behavior matters
* you need mainstream tooling

Consider PyPy when:

* Python-level computation dominates
* the workload is long-running
* JIT optimization is valuable
* dependencies are compatible

The correct engineering question is not:

> Which implementation is universally faster?

It is:

> Which runtime minimizes total system cost for this workload?
