Dictionaries
1. Mapping Model

A dictionary maps keys to values.

user = {
    "name": "Keshav",
    "age": 20,
}

Conceptually:

[
key \rightarrow value
]

2. Hashing

Dictionary lookup approximately performs:

key
 ↓
hash(key)
 ↓
table lookup
 ↓
value

Average lookup:

[
O(1)
]

3. Keys Must Be Hashable

Valid:

{
    "name": "Keshav",
    42: "answer",
    (1, 2): "point"
}

Invalid:

{
    [1, 2]: "value"
}
4. Dictionary Invariants

For a dictionary key:

[
hash(k)
]

must remain consistent while the key participates in the mapping.

More precisely, objects satisfying:

[
a == b
]

must have:

[
hash(a) == hash(b)
]

5. Equality and Hashing

This relationship is crucial.

If:

a == b

then:

hash(a) == hash(b)

must hold.

The reverse is not required.

Hash collisions are allowed.

6. Insertion Order

Modern Python dictionaries preserve insertion order as part of the language specification.

d = {}

d["a"] = 1
d["b"] = 2
d["c"] = 3

print(list(d))

gives:

['a', 'b', 'c']

But ordering semantics do not change the fundamental mapping abstraction.

7. Dictionary Views
d.keys()
d.values()
d.items()

These are dynamic views rather than necessarily independent lists.

8. Dictionary Comprehension
squares = {
    x: x * x
    for x in range(10)
}
Brain-Twisting Questions 🧠
Q1

Suppose:

class User:
    def __init__(self, id):
        self.id = id

    def __eq__(self, other):
        return self.id == other.id

    def __hash__(self):
        return self.id

Now:

u = User(1)
d = {u: "hello"}

u.id = 2

What happens to the dictionary?

Why can the key become effectively "lost"?

Q2

Why is this invariant necessary?

[
a == b \Rightarrow hash(a) == hash(b)
]

Construct a hypothetical dictionary failure if the invariant were violated.

Q3

Two different objects can have:

hash(a) == hash(b)

without:

a == b

Why doesn't this destroy dictionary correctness?