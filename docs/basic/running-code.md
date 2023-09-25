=== "PyScript"

    <p>Once you have <a href="installation">PyScript running on your page</a>, you can start writing Python code inside a <code>&lt;py-script&gt;</code> tag, which will then be executed when the page loads.</p>
    ```html
    <py-script>
        print("Hello, world")
        for i in range(10):
            print(i)  
    </py-script>
    ```
    <p>A complete example of an HTML page which loads PyScript and runs some Python code (including some additional recommended HTML bits) might look like:</p>
    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Hello, world!</title>

        <script defer src="https://pyscript.net/releases/2023.03.1/pyscript.js"></script>
        <link rel="stylesheet" href="https://pyscript.net/releases/2023.03.1/pyscript.css">
    </head>
    <body>
        <py-script>
            print("Hello, world!")
            for i in range(10):
                print(i)
        </py-script>
    </body>
    </html>
    ```


=== "Pyodide"

    <p>Once you have the <a href="installtion">Pyodide script included on your page,</a> you can use the global <a href="https://pyodide.org/en/stable/usage/api/js-api.html#globalThis.loadPyodide">loadPyodide()</a> function in JavaScript to load the Pyodide runtime. Once loaded, the runtime can be used to execute Python code. Note that <code>loadPyodide</code> is an async function, and so must be awaited within another async function in order to retrieve a reference to the runtime once it loads.</p>
    <p>Once loaded, call the <code>runPython()</code> method of the resulting runtime to execute Python code:</p>
    ```js
    async function main() {
        let pyodide = await loadPyodide();
        // Pyodide is now ready to use...
        console.log(pyodide.runPython(`
            import sys
            sys.version
        `));
    };
    main();
    ```
    <p>A complete example of an HTML page with PyScript (including some additional recommended HTML bits) might look like:</p>

    ```html

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Hello, world!</title>

        <script src="https://cdn.jsdelivr.net/pyodide/v0.22.1/full/pyodide.js"></script>
    </head>
    <body>
    <script>
            async function main() {
                let pyodide = await loadPyodide();
                // Pyodide is now ready to use...
                console.log(pyodide.runPython(`
                    import sys
                    sys.version
                `));
            };
            main();
    </script>
    </body>
    </html>
    ```
