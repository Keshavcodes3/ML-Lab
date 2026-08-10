Strings
1. Strings Are Immutable Sequences
name = "Keshav"

A string is an immutable sequence of Unicode characters.

name[0]

returns the first element.

But:

name[0] = "X"

raises an error.

2. Unicode

Python strings represent Unicode text.

text = "नमस्ते"
emoji = "🧠"

Strings are not simply ASCII byte arrays.

3. String vs Bytes
text = "hello"

data = text.encode("utf-8")

print(type(text))
print(type(data))

Result:

str
bytes

Conceptually:

str
 ↓ encode
bytes
 ↓ decode
str
4. Indexing
s = "Python"

print(s[0])
print(s[-1])

Output:

P
n
5. Slicing
s[1:4]

produces:

yth

The general form:

[
[start:stop]
]

6. Strings Are Immutable

This:

s = "hello"
s += " world"

creates a new string object rather than mutating the original string.

Repeated concatenation can therefore have performance implications.

Prefer:

" ".join(parts)

when assembling many pieces.

7. Formatting

Modern Python commonly uses f-strings:

name = "Ada"
age = 36

message = f"{name} is {age}"

Formatting expressions can contain arbitrary expressions:

f"{2 + 3}"
8. Escape Sequences
"\n"
"\t"
"\\"
"\""

Raw strings:

r"C:\Users\Keshav"

are useful when backslashes should not generally be treated as escape sequences.

Brain-Twisting Questions 🧠
Q1

Why does:

"é".encode("utf-8")

produce multiple bytes even though:

len("é")

is:

1

Distinguish:

[
\text{characters}
]

from:

[
\text{encoded bytes}
]

Q2

Predict:

a = "hello"
b = "hello"

print(a == b)
print(a is b)

Can is ever be True here?

Why should you never rely on it?

Q3

What is the performance difference between:

result = ""

for x in items:
    result += str(x)

and:

result = "".join(str(x) for x in items)

What runtime behavior explains the difference?