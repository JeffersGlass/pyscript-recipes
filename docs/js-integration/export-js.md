# Exporting Objects from Python to JS

=== "PyScript"
    !!! abstract ""
        <i>The PyScript (Pyodide) and PyScript(Micropython) version of this recipe are identical, </i>
    <p>In the same way that [`pyscript.window`](import-js.md) can be used to <a href="import-js.html">import JavaScript objects into Python</a>, the same object can be assigned to to create JavaScript objects from Python.</p>
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
    from pyscript import window

    window.a_string = my_string
    window.a_list = [1,2,3]
    window.square_func_from_python = square
    window.some_instance = my_instance
    window.some_class = SimpleClass
    ```

    <p>Notice that we can translate simple objects like strings, and increasingly more complex objects like lists, functions, class instances, and classes. Simple objects like <code>int</code>s, <code>str</code>s, and <code>bool</code>s get converted to their corresponding JavaScript types; anything more complex appears in JavaScript as a proxy for the corresponding Python object. For a complete description of how objects are translated and proxied, see <a href="https://pyodide.org/en/stable/usage/type-conversions.html">the Pyodide Documentation</a>.</p>

    !!! tip
        These examples work regardless of whether the code is run in the main thread or a worker thread - `pyscript.window` always references the global scope of the *main thread*. If you need access to the global scope of a worker thread, use `import js`, which is a proxy for the global scope of the thread the code is running in.

=== "Pyodide"

    <p>In the same way that the `js` pseudo-module can be used to [import JavaScript objects into Python](import-js.md), the same 'module' can be assigned to to create JavaScript objects from Python.</p>
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
    js.a_list = my_list
    js.square_func_from_python = square
    js.some_instance = my_instance
    js.some_class = SimpleClass
    ```

    <p>Notice that we can translate simple objects like strings, and increasingly more complex objects like lists, functions, class instances, and classes. Simple objects like <code>int</code>s, <code>str</code>s, and <code>bool</code>s get converted to their corresponding JavaScript types; anything more complex appears in JavaScript as a proxy for the corresponding Python object. For a complete description of how objects are translated and proxied, see <a href="https://pyodide.org/en/stable/usage/type-conversions.html">the Pyodide Documentation</a>.</p>