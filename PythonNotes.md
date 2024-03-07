# Python notes

- 1.0 [Python Basics](#basics)
  - 1.1 [Clear Terminal Using OS](#clearing-the-python-shell-using-the-os-library)
  - 1.2 [Template literals using F Strings](#template-literals-using-f-strings)
  - 1.3 [Negative indexing](#negative-indexing-in-python)
  - 1.4 [Benefits of the `get()` method](#the-benifits-of-using-the-get-method-on-dictionaries)
  - 1.5 [The use of `*args` and `**kwargs`](#the-use-of-args-and-kwargs)
  - 1.6 [Decorator functions](#decorator-functions)
  - 1.7 [Decorator functions with `*args` and `**kwargs`](#decorator-functions-with-args-and-kwargs)
  - 1.8 [Decorator functions with return value](#decorator-functions-with-return-value)
- 2.0 [Desktop app development]()
  - 2.1 [Tkinter]()
  - 2.3 [Calculator app]()
  - 2.4 [Database desktop app]()
  - 2.5 [Student management system]()
- 3.0 [Utility Tools Development]()
  - 3.1 [File compression / descompression app]()
  - 3.2 [Text-to-speech app]()
  - 3.3 [Password validator]()
  - 3.4 [QR code generator]()
  - 3.5 [Video downloader/mp3 genrartor]()
- 4.0 [Data analysis]()
  - 4.1 [Data analysis basics]()
  - 4.2 [Super market data analysis]()
- 5.0 [Django]()
  - 5.1 [Django basics]()
  - 5.2 [Todo App]()
- 6.0 [Flask]()
  - 6.1 [Flask basics]()
  - 6.2 [Budget Tracker App]()
- 7.0 [Automation]()
  - 7.1 [Web Crawler]()
  - 7.2 [Facebook Auto Poster]()
- 8.0 [Networking]()
  - 8.1 [Networking basics]()
  - 8.2 [Chat app]()
- 9.0 [Image Processing]()
  - 9.1 [Video/image processing]()


## Python basics
Python is a high-level programming language. A high level language is basically a language which is a strong abstraction of instructions for a computer. (Binary code)

Python is a general purpose language which means it can be used for multiple purposes like Desktop apps, Web applications, Data science and Machine learning.

Python used significant indentation. the indentation is part of the syntax which means that you get corrected/get errors if you do not used the correct indentation.

Python is dynamically typed which means that you dont need to specify the type of a variable when you declare it. you can just let the compiler figure out what type of variable it is.

Python is garbage collected which means that it reclaims and memory which allocated by the program but is no longer used which is done automatically.

### Clearing the python shell using the `os` library
You can manipulate the terminal your python is running in using the `os` library but right now we'll just focus on clearing the sceen of trhe terminal that can be done like this using the `os.system()` function so we can directly run commands and then run the command `cls` which is the command for clearing the screen. (cls = clear screen)
```py
import os
os.system('cls')
```

### Template literals using F Strings
You can use template lirterals in python using the regular `print()` function and then add the `f` right before the string and then use the variables in between `{}` brackets to display the value of those variables. Almost everything is allowed in template literals aslongh as the the final value can be displayed as a string.
```py
name = "John"
print(f"Hello {name}, how are you today?")
```

### Negative indexing in python
You can use a negative number to refer to the end of the list and the with every negative increment you move up towards the beginning of the list.
```py
listOfNames = ["John", "Elly", "Robert"]
# listOfNames[0] ->  "John"
# listOfNames[-1] -> "Robert"
# listOfNames[-2] -> "Elly"
```

### List Slicing
You can using list slicing to return a part of a list its the same as refering to an in index instead add a second argument that refers to the index you want to stop slicing. Nagtive numbers can also be used as they also represent a valid postion in the list.
```py
listOfNames = ["John", "Elly", "Robert"]
print(listOfNames[0:2]) # ["John", "Elly"]
``` 

### The benifits of using the `get()` method on dictionaries
There are 2 way to acces to value of a key inside a dictionary `dictionary["key"]` or `dictionary.get("key")` both of these methods result in the value being returned from the specified key. But why do you want to prefer the `get()` method over the use of the standard square brackets `[]`. The reason being that the `get()` method has build in error handling that if it so happens that an error is thrown due to a key not existing inside the dictionary the program will not simply crash and just return `none` whereas trying to access a non-existing key with the square brackets `[]` (directly) it will generate a `KeyError` and the program will crash. Which is ultimately not the desired outcome.

### The use of `*args` and `**kwargs`
Sometimes you want to create a new function that can take a variable amount of arguments. In that case you can use `*args` as a parameter. This will cause your function to accept any amount of parameter even if they are of different types.
```py
def differentTypes(*args):
    print(args)

differentTypes(1,5.4,"Hello",True)  # Output (1, 5.4, 'Hello', True)
```

Additionally if you want to directlyu name your parameters and have them be accessible inside your function you can use the `**kwargs` argument. These are just like args only you need to give each parameter a name as that will serve as the key and you value will serve as your value.

```py
def kwargsFunction(**kwargs): 
    print(kwargs)
    print(kwargs["World"])

kwargsFunction(Hello=2, World={"Universe": False, "World": True})
```
### Decorator functions

### Decorator functions with `*args` and `**kwargs`

### Decorator functions with return value




