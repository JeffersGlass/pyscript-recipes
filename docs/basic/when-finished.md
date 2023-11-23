# Run Code when PyScript Has Finished

=== "PyScript(Pyodide)"
    PyScript emits a [custom event](https://developer.mozilla.org/en-US/docs/Web/Events/Creating_and_triggering_events#creating_custom_events) called "py:all-done" when all PyScript tags on the page have finished executing. To take some action once PyScript has run all its tags, add an event listener for this specific custom event.

    ```py
    <script type="py" worker>
        from pyscript import display, window
        from pyodide.ffi.wrappers import add_event_listener

        def callback(event):
            display("This will run when all script tags are complete")
            display(f"{event.type=}")

        add_event_listener(window, "py:all-done", callback)
    </script>
    ```

    or

    ```html
    <script>
        window.addEventListener("py:all-done", console.log)
    </script>
    ```

    !!! note
        This only applies to PyScript tags that were present on the page at its initial load. Any tags that are added dynamically after the page has loaded will not affect when the `py:all-done` event is dispatched. 

        It does take both `async` and `worker` tags into account.

=== "PyScript (Micropython)"
    PyScript emits a [custom event](https://developer.mozilla.org/en-US/docs/Web/Events/Creating_and_triggering_events#creating_custom_events) called "py:all-done" when all PyScript tags on the page have finished executing. To take some action once PyScript has run all its tags, add an event listener for this specific custom event.

    ```py
    <script type="mpy" worker>
        from pyscript import display, window
    
            def callback(event):
                display("This will run when all script tags are complete")
                display(f"{event.type=}")
    
            window.addEventListener("py:all-done", callback)
    </script>
    ```

    or

    ```html
    <script>
        window.addEventListener("py:all-done", console.log)
    </script>
    ```

    !!! note
        This only applies to PyScript tags that were present on the page at its initial load. Any tags that are added dynamically after the page has loaded will not affect when the `py:all-done` event is dispatched. 

        It does take both `async` and `worker` tags into account.