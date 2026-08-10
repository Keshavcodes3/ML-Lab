# Variables and Bindings

## 1. Python Variables Are Names

The most important mental model:

```text
name ───────► object
```

Not:

```text
variable ───► memory slot containing value
```

Example:

```python
x = 42
```

Conceptually:

```text
namespace
┌──────────┐
│ x ───────┼────► integer object 42
└──────────┘
```

---

# 2. Rebinding

```python
x = 10
x = 20
```

The name changes what it refers to.

It does not mutate the integer `10`.

```text
x ──► 10

x ──► 20
```

The old object may eventually become unreachable.

---

# 3. Aliasing

```python
a = [1, 2]
b = a

b.append(3)

print(a)
```

Output:

```text
[1, 2, 3]
```

Because:

```text
a ─────┐
       ▼
     [1,2,3]
       ▲
b ─────┘
```

---

# 4. Identity

```python
a = []
b = a

print(a is b)
```

Result:

```text
True
```

Identity asks:

> Are these references pointing to the same object?

---

# 5. Equality

```python
a = [1, 2]
b = [1, 2]

print(a == b)
print(a is b)
```

Result:

```text
True
False
```

Two distinct objects can have equal values.

---

# 6. Multiple Assignment

```python
a = b = c = 0
```

Conceptually:

```text
a ─┐
b ─┼──► 0
c ─┘
```

For immutable objects this is usually harmless.

For mutable objects:

```python
a = b = []
```

both names refer to the same list.

---

# 7. Chained Assignment Trap

```python
a = b = []
a.append(1)

print(b)
```

Result:

```text
[1]
```

Because there is one list.

---

# 8. Augmented Assignment

```python
x += 1
```

does not universally mean:

```python
x = x + 1
```

The object can implement `__iadd__`.

For mutable objects:

```python
x += y
```

may mutate `x`.

For immutable objects, a new object may be produced.

---

# Brain-Twisting Questions 🧠

### Q1

What happens?

```python
a = [1, 2]
b = a

a += [3]

print(a)
print(b)
print(a is b)
```

Now compare:

```python
a = [1, 2]
b = a

a = a + [3]

print(a)
print(b)
print(a is b)
```

Why are the results different?

---

### Q2

Predict:

```python
a = b = []
c = []

print(a is b)
print(a is c)
print(a == c)
```

Explain every result from object identity rather than memorization.

---

### Q3

What exactly happens here?

```python
x = object()
y = x
x = None
```

When does the original object become unreachable?

What references exist at each step?
