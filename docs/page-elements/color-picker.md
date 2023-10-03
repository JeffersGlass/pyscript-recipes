# Color Picker

<p>Modern browsers have the ability to add a simple color picker directly to your HTML, using <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/color"><code>&lt;input type="color"&gt;</code></a> If your browser supports one, it looks like this:</p>
<p><input type="color" id="main-color" py-input="do_something_with_color()" py-change="do_something_else()"></p>
<p>The html for this element looks like this:</p>

```html
<input type="color" id="main-color">
```

<p>There are several events one can listen to react to the user changing color, including:</p>
<ul>
    <li><a href="https://developer.mozilla.org/en-US/docs/Web/API/Element/click_event"><code>click</code></a> - fires when the user first clicks on the element to open the color picker</li>
    <li><a href="https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/input_event"><code>input</code></a> - fires whenever the user selects a new color within the color picker</li>
    <li><a href="https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/change_event"><code>change</code></a> - fires when the user deselects/closes the color picker</li>
</ul>

=== "PyScript"

    <p>To listen for these events in PyScript, add an attribute called <code>py-[event]</code> to the <code>input</code> object, where <code>[event]</code> is the type of one of these events above.</p>
    <p>For example, the following code prints:</p>
    <ul>
        <li>An acknowledgement that the user opened the color picker</li>
        <li>The selected color whenver the color is changed</li>
        <li>The 'final' selected color when the color picker is closed</li>
    </ul>

    ```html
    <input type="color" 
        id="main-color" 
        py-click="opened_picker"
        py-input="color_changed" 
        py-change="final_color">
    ```

    ```py
    from pyscript import display, document

    def opened_picker(*args):
        display("You opened the color picker!")

    def color_changed(*args):
        elem = document.getElementById("main-color")
        value = elem.value
        display(f"The color changed to: {value}")

    def final_color(*args):
        elem = document.getElementById("main-color")
        value = elem.value
        display(f"The selected color is: {value}")
    ```


=== "Pyodide"

    <p>To listen for these events in Pyodide, once <a href="/basic/installation">Pyodide is loaded,</a>, use Pyodide's <a href="https://pyodide.org/en/stable/usage/api/python-api/ffi.html#pyodide.ffi.wrappers.add_event_listener"><code>add_event_listener</code></a> function to attach the appropraite event listeners to the <code>&lt;input&gt;</code> element.</p>
    <p>For example, the following code prints:</p>
    <ul>
        <li>An acknowledgement that the user opened the color picker</li>
        <li>The selected color whenver the color is changed</li>
        <li>The 'final' selected color when the color picker is closed</li>
    </ul>
    ```html
    <input type="color" id="main-color" >
    ```
    <p>The following Python code should be run using <code>pyodide.runPython</code>:</p>

    ```py
    import js
    from pyodide.ffi.wrappers import add_event_listener

    def opened_picker(event):
        print("You opened the color picker!")

    def color_changed(event):
        value = event.target.value
        print(f"The color changed to: {value}")

    def final_color(event):
        value = event.target.value
        print(f"The selected color is: {value}")

    elem = js.document.getElementById("main-color")
    add_event_listener(elem, 'click', opened_picker)
    add_event_listener(elem, 'input', color_changed)
    add_event_listener(elem, 'change', final_color)
    ```