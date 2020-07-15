---
title: Introduction to Python
category: Tutorials
order: 12
---

<a href="https://colab.research.google.com/drive/13rU3LTRTmv0JDUBxsH8DJmziqYOS8UCn" target="_parent"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>



## Types


```python
my_var = "this is a string"
my_var = 4
my_var = [3, 4, 5]
my_var = {"hello": "world"}
```

## Variables


```python
a = 1
b = 4
print(a + b)
```

    5


## Functions


```python
def add_numbers(x, y):
    z = x + y
    return z

add_numbers(1, 4)
```




    5



## For-Loops


```python
my_array = [2, 4, 6, 8, 10]

for i in my_array:
    z = i + 10
    print(z)
```

    12
    14
    16
    18
    20


## Dictionaries


```python
my_dict = {"name": "Matt", "age": 32, "height": "6 foot"}

print(my_dict['name'])
print(my_dict['age'])
```

    Matt
    32


## Classes


```python
class Dog:
    def __init__(self):
        self.bark = "woof"

    def make_noise(self):
        print(self.bark)


new = Dog()
new.make_noise()
```

    woof



```python

```
