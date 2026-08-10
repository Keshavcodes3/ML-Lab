Booleans and None
1. Boolean Values

Python has two boolean singleton objects:

True
False

Boolean expressions include:

x > 10
x == y
x is None
2. Truthiness

Python does not require values to literally be booleans in conditions.

if value:
    ...

Python asks whether value is truthy.

Common falsy values include:

False
None
0
0.0
""
[]
{}
set()

Most other objects are truthy by default.

3. Custom Truthiness

A class can define:

__bool__

or:

__len__

Example:

class UserCollection:
    def __len__(self):
        return 0

Then:

bool(UserCollection())

is:

False
4. None

None represents the absence of a value.

result = None

Use:

result is None

rather than:

result == None

because identity is the appropriate semantic test for the singleton.

5. Short-Circuit Evaluation
a and b

does not necessarily evaluate both expressions.

Likewise:

a or b

can stop early.

Example:

x = None

result = x or "default"
6. and and or Return Operands

This is important.

print(10 and 20)

returns:

20

while:

print(0 and 20)

returns:

0

They do not necessarily return True or False.

Brain-Twisting Questions 🧠
Q1

Predict:

x = [] or [1]
y = [1] and []
z = [] and 100

print(x)
print(y)
print(z)

Why are the results not booleans?

Q2

What gets executed?

def expensive():
    print("EXPENSIVE")
    return True

False and expensive()

Why?

Q3

What happens?

class A:
    def __bool__(self):
        print("checking")
        return False

x = A()

if x:
    print("yes")

When exactly is __bool__ invoked?