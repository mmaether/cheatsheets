# Python

## Basics

This section outlines basic Python syntax.

### Variables

```py
var = 'Hello'
```

### Comments

```py
# This is a comment

"""
This is a multiline comment.
"""
```

### Print Function

```py
print('Hello world')
```

### Input Function

```py
print('What is your name?')
myName = input()
print('Hi, ' + myName)

# What is your name?
# Frank
# Hi Frank
```

### Length Function

```py
len('hello')
# 5
```

## Control Flow

### If Statements

```py
name = 'Frank'

if name == 'Frank':
  print('Hi Frank')
elif name == 'Georgie':
  print('Howdie Georgie')
else:
  print('Hello stranger')

# Hi Frank
```

### Switch Case

```py
response_code = 201

match response_code:
  code 200:
    print('OK')
  code 404:
    print('404 Not Found')
  code 500:
    print('Internal Server Error')
  code 502:
    print('502 Bad Gateway')
```

### While Loop

```py
i = 0
while i < 5:
  print('Hello, world.')
  i = i + 1

# Hello, world.
# Hello, world.
# Hello, world.
# Hello, world.
# Hello, world.
```

### For Loop

```py
pets = ['Rover', 'Gizmo', 'Spot']
for pet in pets:
    print(pet)

# Rover
# Gizmo
# Spot
```

### Range

```py
for i in range(5):
  print(i)
W
# 0
# 1
# 2
# 3
# 4
# 5
```

## Functions

```py
def hello(name):
  print('Hello ' + name)

hello('Alice')
# Hello Alice
```

Installing 3rd party modules:
[https://www.youtube.com/watch?v=lvm6Q3SBJEk](https://www.youtube.com/watch?v=lvm6Q3SBJEk)

## VS Code

- [Getting Started with Python in VS Code](https://code.visualstudio.com/docs/python/python-tutorial)
- [Python in Visual Studio Code](https://code.visualstudio.com/docs/languages/python)