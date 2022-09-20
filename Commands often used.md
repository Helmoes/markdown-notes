# in powershell:
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser


```powershell
py --version
```

In VSC terminal:
replace .venv with name of new virtual environment
```powershell
py -3 -m venv .venv 
.venv\scripts\activate
deactivate
```


```powershell
pcc-env\Scripts\activate
```


install python packages in CURRENT environment.
This should be done in the virtual environment.
Example here is matplotlib.
```powershell
py -m pip install matplotlib
py -m pip install SomePackage==1.0.4    # specific version
py -m pip install "SomePackage>=1.0.4"  # minimum version
py -m pip install --upgrade SomePackage # to explicitly upgrade a package
```

```powershell
py -m pip_autoremove jupyter
py -m pip uninstall -y jupyter jupyter_core jupyter-client jupyter-console jupyterlab_pygments notebook qtconsole nbconvert nbformat jupyterlab-widgets nbclient
```

```powershell
py -m pip list
py -m pip freeze > requirements.txt
py -m pip uninstall -r requirements.txt
```

```powershell
py -m pip install --upgrade pip
py -m pip install --upgrade pip setuptools wheel
```


# strings
```python
str.strip()
s = ("this is a very"
     "long string too"
     "for sure ..."
    )
```

# Check type
```python
type(variableName)
isinstance(variableName, type)
```

# lists
```python
listname = [element1, element2]
listname[0] = newelement # editing list element
listname.append(newelement)
listname.insert(index, newelement)
del listname[index]
listname.pop() # pops last element
listname.pop(index)
listname.remove(element) # removes first occurrence of element in list
listname.sort(reverse=False)
sorted(listname)
listname.reverse()
len(listname)
for element in listname:
    print(element)

range(start, stop[, step])
listname = list(range(1, 6))
```

Use 'in' and 'not in' to check if element is (not) in list.

**slicing:** leave out a for all elements up until b-1, leave out b for elements from a until end.
use negative index for elements from end.
```python
list_slice = listname[a:b] 
copyof_listname = listname[:]
```

# tuple

```python
tuplename = (a, b, ..)
```


# if-statements
```python
if conditional_test:
    ...
else:
    ...
```

# dictionaries
```python
dict_name = {'key1' : value1, 'key2' : value2}

favorite_languages = {
    'jen': 'python',
    'sarah': 'c',
    'edward': 'ruby',
    'phil': 'python',
    }
```

adding new key-pairs
```python
dict_name['newkey3'] = value3
dict_name['newkey4'] = value4
```

modifying values of existing keys
```python
dict_name['key1'] = newvalue1
del dict_name['key1']
point_value = alien_0.get('points', 'No point value assigned.') # for when the key-value pair might not exist

for key, value in dict_name.items():
    ...

for key in dict_name.keys(): # is same as
for key in dict_name:
```

while on list to move items until list is empty
```python
while listname:
    current_item = listname.pop()
    newlist.append(current_item)
```

# functions
```python
def function_name(arg1 = default_value1, arg2 = default_value2):
    ...
    return return_value #optional
```

```python
Aligned with opening delimiter.
foo = long_function_name(var_one, var_two,
                         var_three, var_four)

function_name(arg1, arg2) # positional arguments: must be in correct order
function_name(arg2 = ..., arg1 = ...) # keyword arguments: order doesn't matter
```

variable number of arguments
```python
def function_name(arg1, arg2, *args, **kwargs):
    # args is a tuple: for varying number of positional arguments
    # kwargs is a dictionary: for varying number of keyword arguments

    if len(args) ==1:
        values = args[0]
    else:
        values = args
    
    if len(values) == 0:
        raise ValueError('function_name() args is an empty sequence')
```

```python
def function_name(
        parameter_0, parameter_1, parameter_2,
        parameter_3, parameter_4, parameter_5):
    function body...
```

# importing modules

```python
from module_name import function_name as fn
```


# OOP

```python
class ClassName:
    pass # body placeholder

class ClassName:

    # class variables, shared between all instances
    class_var1 = ...

    def __init__(self, arg1, arg2, ...):
        # define attributes/instance variables
        self.arg1 = arg1
        self.arg2 = arg2

    def method1(self):
        # use self.attr1 etc to make methods
        return ...

    @classmethod
    def class_method1(cls, arg1):
        cls.class_var1 = arg1

    @staticmethod
    def static_method1(..., ...):
        ...
```


```python
object1 = ClassName(arg1, arg2, ...)
object1.__dict__ # returns all variable of object1
help(object1)
dir(func)
FullArgSpec(args, varargs, varkw, defaults, kwonlyargs, kwonlydefaults, annotations) = inspect.getfullargspec(func)
```

## subclasses
```python
class SubClassName(ClassName):

    # subclass variables

    def __init__(self, arg1, arg2, subarg1)
        super().__init__(arg1, arg2)

with open('text_file.txt') as f:
    contents = f.read()

with open(output_file, 'w') as of:
    of.write("string")
```