# Importing Python Objects in JavaScript

It may be useful for some applications to extract objects from Python via JavaScript by name. This is, in generally, a little messier than [exporting objects from Python directly](export-js.md), but for some use cases it may be necessary

=== "PyScript"
    !!! abstract ""
        <i>The PyScript (Pyodide) and PyScript(Micropython) version of this recipe are identical, </i>

    We can use an alternate way of loading PyScript to install a hook, which stores a reference to the interpreter for later use. In this case, we'll store a global reference to the interpreter by assigning to the `window` object.
    !!! info

        The following code can *replace* the [typical script tag](../basic/installation.md) that would be used to load PyScript. Or they can be used together, if their URLs match; the PyScript module will only be imported once regardless.

    ```js
    <script type="module">
        import { config, hooks } from "https://pyscript.net/releases/2023.12.1/core.js"
        hooks.onInterpreterReady.add((wrap, element) => {
            window.pyInterpreter = wrap.interpreter
        })
    </script>

    <script type="py">
        my_string = "Hello, world!"
    </script>
    ```
    

    Once stored, we can access Python objects by name by using (in this case) `pyInterpreter.globals.get(name)`:


    ```html
    <button onclick="console.log(pyInterpreter.globals.get('my_string'))">Click Me</button>
    ```

    !!! warning
        Retrieving values from the interpreter will only succeed once the interpreter has been initialized and its code has run. You may wish to [listen for the `py:all-done`]() event and only act when the interpreter is ready.

=== "Pyodide"

    Once Pyodide <a href="/basic/installation">has been loaded</a>, we can extract objects from its global scope. If we have objects in the Python global scope, we can extract them in JavaScript using <code>pyodide.globals.get(...)</code>:

    ```js
    async function main() {
        let pyodide = await loadPyodide();
        // Pyodide is now ready to use...
        console.log(pyodide.runPython(`
            my_string = "Hello again"
        `));

        const s = pyodide.globals.get('my_string')
        console.log(s) #logs hello again
    };
    main(); 
    ```