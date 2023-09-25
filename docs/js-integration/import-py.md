# Importing Python Objects in JavaScript

<p>It may be useful for some applications to extract objects from Python via JavaScript.</p>

=== "PyScript"

    Once PyScript <a href="/basic/installation">has been loaded</a>, we can extract objects from its global scope. If we have objects in the Python global scope:

    ```py
    my_string = "Hello again"  
    ```

    We can retrieve a reference to this Python object by name using <code>pyscript.interpreter.globals.get(name)</code>:

    ```html
    <button onclick="console.log(pyscript.interpreter.globals.get('my_string'))">Click Me</button>
    ```

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