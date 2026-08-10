Numbers

Python provides several numerical types.

int
float
complex
bool

There are also numerical types in the standard library such as:

decimal.Decimal
fractions.Fraction
1. Integers
x = 123

Python integers have arbitrary precision.

Unlike fixed-width machine integers:

int32 → overflow possible
int64 → overflow possible
Python int → grows as needed

Example:

x = 10 ** 1000

print(len(str(x)))
2. Integer Arithmetic
a = 10
b = 3

print(a + b)
print(a - b)
print(a * b)
print(a / b)
print(a // b)
print(a % b)
print(a ** b)

Important:

/   → true division
//  → floor division
3. Floor Division Is Actually Floor
print(7 // 3)

gives:

2

But:

print(-7 // 3)

gives:

-3

because:

[
\lfloor -7/3 \rfloor = -3
]

It is not truncation toward zero.

4. Floating Point

Python float generally uses IEEE 754 double precision.

Therefore:

0.1 + 0.2

may produce:

0.30000000000000004

because:

[
0.1_{10}
]

cannot be represented exactly in binary floating point.

5. Floating Point Is Approximation
x = 0.1

does not mean:

[
x = \frac{1}{10}
]

exactly.

It means:

[
x \approx \frac{1}{10}
]

represented using a finite binary format.

6. Complex Numbers
z = 3 + 4j

print(z.real)
print(z.imag)

Python uses:

j

for the imaginary unit.

7. Boolean Is an Integer Subclass
print(isinstance(True, int))

Result:

True

Historically and structurally:

bool
  ↓
int

Therefore:

True + True

produces:

2

This is legal but should be used deliberately.

8. Numeric Equality

Interesting:

1 == 1.0

is:

True

But:

1 is 1.0

is:

False

Equality and identity remain distinct.

Brain-Twisting Questions 🧠
Q1

Predict:

print(-7 // 3)
print(-7 % 3)

Why must these satisfy:

[
a = bq + r
]

with Python's chosen (q) and (r)?

Q2

Why can this happen?

print(0.1 + 0.2 == 0.3)

Explain it in terms of binary representation rather than saying "floating point is inaccurate."

Q3

What does this produce?

x = 10**1000
y = x + 1

print(y - x)

Why doesn't integer overflow occur?