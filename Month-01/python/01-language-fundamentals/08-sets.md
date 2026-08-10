Sets
1. Mathematical Set Semantics

A set represents unique elements.

s = {1, 2, 3}

Duplicate insertion:

{1, 1, 2, 2}

results in:

{1, 2}
2. Hash-Based Representation

Sets are generally implemented using hash tables.

Conceptually:

hash(x)
   ↓
bucket/probe
   ↓
membership

Therefore average membership is approximately:

[
O(1)
]

while pathological cases can degrade.

3. Membership
if user_id in user_ids:
    ...

This is usually much faster than scanning a list for large collections.

4. Set Algebra
a = {1, 2, 3}
b = {3, 4, 5}

a | b
a & b
a - b
a ^ b

Represent:

union
intersection
difference
symmetric difference
5. Hashability

Set elements must be hashable.

Valid:

{1, "hello", (1, 2)}

Invalid:

{[1, 2]}

because lists are mutable and unhashable.

6. Sets Are Not Ordered Sequences

Do not design logic around an observed iteration order.

Even if a particular runtime/version produces stable-looking output, set semantics do not promise sequence ordering.

Brain-Twisting Questions 🧠
Q1

Why does mutability conflict with hashability?

Suppose:

x = [1, 2]

and imagine Python allowed:

set([x])

What invariant could break if x later mutated?

Q2

Given:

a = {1, 2, 3}
b = {3, 4, 5}

derive the result of:

a ^ b

using set algebra rather than memorization.

Q3

If set lookup is average (O(1)), why isn't it "always O(1)"?

What assumptions are hidden inside average-case hashing complexity?