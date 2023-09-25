<p>In PyScript and Pyodide, the pseudo-module <code>js</code> is a proxy for the <a href="https://developer.mozilla.org/en-US/docs/Glossary/Global_object">JavaScript Global Scope</a>. That is to say, if we have an variable in the JavaScript global scope:</p>

```html
<script>
    // Create a JavaScript global variable called my_string
    var my_string = "Hello, world"
</script>
```

<p>We can access it (and in this case, print the string it represents) using either any of the following Python syntax options:</p>

```py
import js
print(js.my_string)
```


```py
from js import my_string
print(my_string)
```

<p>Using <code>from js import *</code> does <i>not</i> work; however, you can get a list of all objects in the JavaScript global scope using:</p>

```py
import js
print(dir(js))
```
