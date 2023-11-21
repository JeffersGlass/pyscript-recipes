# Running Code

=== "PyScript (Pyodide)"

    <p>Once you have <a href="installation">PyScript running on your page</a>, you can start writing Python code inside a <code>&lt;script&gt;</code> tag with the attribute `type="py"`, which will then be executed when the page loads.</p>
    ```html
    <script type="py">
        print("Hello, world")
        for i in range(10):
            print(i)  
    </script>
    ```
    !!! info

        Note that Python's `print` function outputs to the [browser's dev console](https://balsamiq.com/support/faqs/browserconsole/). To output content to the screen, use PyScript's [display function](https://docs.pyscript.net/2023.11.1/user-guide/#pyscriptdisplay)
    <p>A complete example of an HTML page which loads PyScript and runs some Python code (including some additional recommended HTML bits) might look like:</p>
    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <title>Hello, world!</title>
        <script type="module" src="https://pyscript.net/releases/2023.11.1/core.js"></script>
    </head>
    <body>
        <script type="py">
            print("Hello, world!")
            for i in range(10):
                print(i)
        </script>
    </body>
    </html>
    ```

=== "PyScript (Micropython)"

    <p>Once you have <a href="installation">PyScript running on your page</a>, you can start writing Python code inside a <code>&lt;script&gt;</code> tag with the attribute `type="mpy"`, which will then be executed when the page loads.</p>
    ```html
    <script type="mpy">
        print("Hello, world")
        for i in range(10):
            print(i)  
    </script>
    ```
    !!! info

        Note that Python's `print` function outputs to the [browser's dev console](https://balsamiq.com/support/faqs/browserconsole/). To output content to the screen, use PyScript's [display function](https://docs.pyscript.net/2023.11.1/user-guide/#pyscriptdisplay)
    <p>A complete example of an HTML page which loads PyScript and runs some Python code (including some additional recommended HTML bits) might look like:</p>
    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <title>Hello, world!</title>
        <script type="module" src="https://pyscript.net/releases/2023.11.1/core.js"></script>
    </head>
    <body>
        <script type="mpy">
            print("Hello, world!")
            for i in range(10):
                print(i)
        </script>
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
            print(sys.version)
        `));
    };
    main();
    ```
    !!! info

        Note that Python's `print` function outputs to the [browser's dev console](https://balsamiq.com/support/faqs/browserconsole/).
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
                    print(sys.version)
                `));
            };
            main();
    </script>
    </body>
    </html>
    ```
