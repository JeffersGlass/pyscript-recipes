=== "PyScript (Pyodide)"

    Add a <code>&lt;py-editor&gt;</code> tag anywhere on your page to create an editable, runnable code-editor on the page:
    ```html
    <py-editor>
        # Text inside the editor is pre-populated
        for i in range(5):
            print(i)
    </py-editor>
    ```

    !!! info ""
    Editors are a worker-only feature - you will need to conigure your server to use the appropriate headers, or use a shim like [mini-coi.js](https://github.com/webreflection/mini-coi).

    **ENV**

    By default, all `py-editor`s of a given type willl reuse the same interpreter/worker. To separate different editors or groups of editors into using different interpreters, use the named `env` attribute:

    ```html
    <py-editor env="first">
        x = 0
    </py-editor>

    <py-editor env="first">
        print(x) # Works fine; uses the 'first' interpreter
    </py-editor>

    <py-editor env="second">
        print(x) # Fails: 'second' is a while different Pyodide interpreter.
    </py-editor>
    ```

=== "PyScript (Micropython)"

    Add a <code>&lt;mpy-editor&gt;</code> tag anywhere on your page to create an editable, runnable code-editor on the page:
    ```html
    <mpy-editor>
        # Text inside the editor is pre-populated
        for i in range(5):
            print(i)
    </mpy-editor>
    ```

    !!! info ""
    Editors are a worker-only feature - you will need to conigure your server to use the appropriate headers, or use a shim like [mini-coi.js](https://github.com/webreflection/mini-coi).

    **ENV**

    By default, all `mpy-editor`s of a given type willl reuse the same interpreter/worker. To separate different editors or groups of editors into using different interpreters, use the named `env` attribute:

    ```html
    <mpy-editor env="first">
        x = 0
    </mpy-editor>

    <mpy-editor env="first">
        print(x) # Works fine; uses the 'first' interpreter
    </mpy-editor>

    <mpy-editor env="second">
        print(x) # Fails: 'second' is a while different Pyodide interpreter.
    </mpy-editor>
    ```