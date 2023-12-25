=== "PyScript"

    There is no need to install anything on your computer to use PyScript.
    Inside your HTML document, include the following tag. Ideally, this should go inside your `<head>` tag, but it is also fine to put them inside the  `<body>` tag:

    ```html
    <script type="module" src="https://pyscript.net/releases/2023.12.1/core.js"></script>
    ```

    This tag is the same whether you intend to use the Pyodide (CPython) interpreter or Micropython.
    
=== "Pyodide"

    There is no need to install anything on your computer to use Pyodide.
    Inside your HTML document, include the following tags. Ideally, this should go inside your <code>&lt;head&gt;</code> tag, but it is also fine to put it inside the <code>&lt;body&gt;</code> tag:

    ```html
    <script src="https://cdn.jsdelivr.net/pyodide/v0.24.1/full/pyodide.js"></script>
    ```