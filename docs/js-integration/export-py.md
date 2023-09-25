<p>It may be useful for some applications to create new Python objects directly from JavaScript.</p>

=== "PyScript"

    <!-- In PyScript next, this has issue with Syncify-->
    <p>Once PyScript <a href="/basic/installation">has been loaded</a>, we can use JavaScript to directly create Python objects using <code>pyodide.globals.set(name, value)</code>:</p>

    ```html
    <button onclick="pyscript.interpreter.globals.set('my_string', 'hello world!')">Click Me</button>
    ```

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