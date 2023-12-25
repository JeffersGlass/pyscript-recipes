# Exporting Objects from JS to Python

<p>It may be useful for some applications to create new Python objects directly from JavaScript.</p>

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

        var my_js_array = [1,2,3,4]
    </script>
    ```
    

    Once stored, we can create Python proxies of JavaScript objects by using `pyInterpreter.globals.set(name, value)`:


    ```html
    <button onclick="console.log(pyInterpreter.globals.get('myArray', my_js_array))">Click Me</button>
    ```

    !!! warning
        Retrieving values from the interpreter will only succeed once the interpreter has been initialized and its code has run. You may wish to [listen for the `py:all-done`]() event and only act when the interpreter is ready.


=== "Pyodide"

    <p>Once Pyodide <a href="/basic/installation">has been loaded</a>, we can use JavaScript to directly create Python objects using <code>pyodide.globals.set(name, value)</code>:</p>

    ```js
    async function main() {
        let pyodide = await loadPyodide();

        const s = 'hello world'
        pyodide.globals.set('my_string', s)

        // Pyodide is now ready to use...
        pyodide.runPython(`
            print(my_string)
        `);
    };
    main(); 
    ```