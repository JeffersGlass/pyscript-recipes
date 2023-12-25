=== "PyScript (Pyodide)"

    PyScript can automatically load [JavaScript (ECMAScript) modules](https://nodejs.org/api/esm.html) and make them available for import in Python, using the `js_modules` table in `<py-config>`. The table has two subtables, `main` and `worker`, each of which is a list of `URL: python_name` pairs:

    ```html
    <py-config>
        [js_modules.main]
        "https://cdn.jsdelivr.net/npm/fireworks-js@2.10.7/+esm" = "Fireworks"
        
        [js_modules.worker]
        "import mathjax from 'https://cdn.jsdelivr.net/npm/mathjax@3.2.2/+esm" = "Mathjax"
    </py-config>
    ```

    The location specifier (`main` or `worker`) specifies where the *ESM module itself* is loaded. Modules loaded on the main thread are available to Python running on both the main thread and in workers. Most modules should likely be loaded to the main thread if their authors assume they'll have access to the DOM.

    Once included, modules can be imported within Python as a submobule of the `polyscript.js_modules`, [constructed](constructing-js-objects.md) and [interacted with](fundamentals.md) like any other JavaScript object.

    !!! info
        The `polyscript.js_modules` package will change to `pyscript.js_modules` in a future release.

    **Example**

    ```html
    <div id="fw"></div>

    <py-config>
        [js_modules.main]
        "https://cdn.jsdelivr.net/npm/fireworks-js@2.10.7/+esm" = "Fireworks"
    </py-config>

    <script type="py">
        # Import ESM module just like a Python module
        from polyscript.js_modules import Fireworks

        # Start fireworks on the page
        from pyscript import document
        container = document.getElementById("fw")
        f = Fireworks.Fireworks.new(container)
        f.start()
    </script>
    ```
    
=== "PyScript (Micropython)"

    This feature is not yet available in Micropython, but will be integrated in an upcoming release.