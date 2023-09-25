# Exporting Objects from Python to JS

<p>In the same way that the <code>'js module'</code> can be used to <a href="import-js.html">import JavaScript objects into Python</a>, the same 'module' can be assigned to to create JavaScript objects from Python.</p>
<p>If we have some Python objects that we'd like to export as a JavaScript objects:</p>

```py
my_string = "This sure is a string"
my_list = [1,2,3]

def square(x):
    return x * x

class SimpleClass:
    def __init__(self, name):
        self.name = name
    
my_instance = SimpleClass("some name")
```

<p>We can use the following Python syntax to create corresponding JavaScript objects:</p>

```py
import js

js.a_string = my_string
js.a_list = [1,2,3]
js.square_func_from_python = square

class SimpleClass:
    def __init__(self, name):
        self.name = name
    
my_instance = SimpleClass("some name")

js.some_instance = my_instance
js.some_class = SimpleClass
```

<p>Notice that we can translate simple objects like strings, and increasingly more complex objects like lists, functions, class instances, and classes. Simple objects like <code>int</code>s, <code>str</code>s, and <code>bool</code>s get converted to their corresponding JavaScript types; anything more complex appears in JavaScript as a proxy for the corresponding Python object. For a complete description of how objects are translated and proxied, see <a href="https://pyodide.org/en/stable/usage/type-conversions.html">the Pyodide Documentation</a>.</p>