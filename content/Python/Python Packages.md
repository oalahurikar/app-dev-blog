
What is python packages?

---
If your package contains a module with functions you want to import, you can use the * wildcard to import all functions from that module.

```python
my_package/
  __init__.py
  module1.py
  module2.py
```
Assume module1.py has the following functions:
```python
# module1.py
def func1():
    pass

def func2():
    pass
```
To import all the functions from module1, you would do the following in your script:
```python
from my_package.module1 import *
```

OR
**Importing Specific Functions from a Package**
```python
from my_package.module1 import func1, func2
```

---

What is __init__.py file, what does it do?


```python
__init__.py
```


utils???
- All different functions not related together can go to utils