# Pure Diciplined FISH

A guide to corretly writing functional programming. 


## Pure Functions
---
Function always returns the same result when the same parameters are passed.

```python
scary_global_state = 3432


# Always returns passed in value times 2
def foo(a: int):
    return a * 2

# Return value depends on scary_global_state
def bar(a: int):
    return a * scary_global_state
```


## Disciplined State
---
No sharing of a mutatable state.

```python
scary_global_state = 3432


# Mutates the scary_global_state 
def foo(a: int):
    scary_global_state =+ 1
    return a * 2

# Return value depends on scary_global_state
def bar(a: int):
    return a * scary_global_state
# which depends on how many times `foo` is called
```


## Functional Composition
---
Calling a function on the return value of another, thus "composing" functions. 

```python
def momma():
    return "Momma, "


def just_killed_a_man(val: str):
    return f"{val}just killed a man, "


def put_a_gun_against_his_head(val: str):
    return f"{val}put a gun against his head"


first_line = put_a_gun_against_his_head(
    just_killed_a_man(
        momma()
    )
)

# Guess what this prints
print(first_line)
```


## Immutability
---
Avoid mutating values, FP languages have amazing features for handling
collections (mapping, sorting, filtering ext.) so it's rarely needed.  

```python
original_list = [0, 1, 2, 3, 4]

even_numbers = []

# This works, but takes a while
for item in list:
    if item % 2 == 0:
        original_list.append()

# This is way quicker
even_numbers = [num for num in original_list if num % 2 == 0]
```


## Side effects (avoid/reduce)
---
When a function has an effect on the overall state, I.E. changing 
something about the environment like a file. Obviously this will be needed
eventually but it should be reduced to a few designated and well handled 
functions/modules. 

```python
# This always returns a tuple of (Boolean, string) no matter what 
def encapsulated_file_read():
    try:
        f = open("demofile.txt", "r")
        return (True, f.read())
    except:
        (False, "")

(sucess, file_data) = encapsulated_file_read()

if success:
    print(file_data)
else:
    print("Couldn't open file. ")

```


## Higher Order Functions
---
Functions that can take or return other functions as parameters/return types,
an example of this is currying. 

__Currying__:
```python
def multiplier(a: int):
    def inner(b: int):
        return a * b
    return inner

result = multiplier(5)(2)

# Prints 10
print(result)
```

