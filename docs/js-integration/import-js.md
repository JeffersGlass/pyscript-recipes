=== "PyScript"
    !!! abstract ""
        <i>The PyScript (Pyodide) and PyScript(Micropython) version of this recipe are identical, </i>

    In PyScript, the object `window` in the `pyscript` namespace is a proxy for the <a href="https://developer.mozilla.org/en-US/docs/Glossary/Global_object">JavaScript Global Scope</a> of the *main thread* That is to say, if we have an variable in the JavaScript global scope of the main (window) thread:

    ```html
    <script>
        // Create a JavaScript global variable called my_string
        var my_string = "Hello, world"
    </script>
    ```

    We can access it (and in this case, print the string it represents) using either any of the following Python syntax options:

    ```py
    import pyscript
    print(pyscript.window.my_string)
    
    ```
    or 

    ```py
    from pyscript import window
    print(window.my_string)
    ```

    !!! tip
        These examples work regardless of whether the code is run in the main thread or a worker thread - `pyscript.window` always references the global scope of the *main thread*. If you need access to the global scope of a worker thread, use `import js`, which is a proxy for the global scope of the thread the code is running in.

=== "Pyodide"

    <p>In Pyodide, the pseudo-module <code>js</code> is a proxy for the <a href="https://developer.mozilla.org/en-US/docs/Glossary/Global_object">JavaScript Global Scope</a> of the thread the code is currently running in. That is to say, if we have an variable in the JavaScript global scope:</p>

    ```html
    <script>
        // Create a JavaScript global variable called my_string
        var my_string = "Hello, world"
    </script>
    ```

    <p>We can access it (and in this case, print the string it represents) using either any of the following Python syntax options:</p>

    ```py
    import js
    print(js.my_string)
    ```

    ```py
    from js import my_string
    print(my_string)
    ```
