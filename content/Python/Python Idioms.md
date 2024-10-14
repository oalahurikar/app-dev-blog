
`if __name__ == '__main__':` What this does, and why use this?

**What It Does**
• This line checks whether the script is being run directly or imported.
• If the script is run directly, the condition is true (__name__ == '__main__'), and the block of code under it will execute.
• If the script is imported as a module in another script, this block of code is skipped.

**Why It’s Useful**
1. **Running as a Script vs. Importing as a Module**:
• Sometimes, you may write a Python file that can either be executed on its own or imported into another script. For example, you might have utility functions or classes that you want to reuse in multiple scripts.
• The if __name__ == '__main__': construct allows you to run certain code only when the script is executed directly, without it being triggered when the module is imported elsewhere.

2. **Organizing Code**:
• You might use this construct to define code that tests or demonstrates how to use the functions and classes in the module.
• Example: If you are writing a library or utility, you can include some example usage or testing code within this block, but ensure that when the module is imported, this code is not executed.

Example use
```python
# my_module.py
def greet(name):
    return f"Hello, {name}!"

# Code below will only run if the script is executed directly
if __name__ == '__main__':
    # This will only be executed if the file is run directly
    print(greet("Alice"))  # Output: Hello, Alice!
```

---
