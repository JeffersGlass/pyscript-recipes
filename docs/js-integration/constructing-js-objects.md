!!! abstract ""
    <i>The PyScript and Pyodide versions of this recipe are identical</i>

<p>Python lacks the <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new"><code>new operator</code></a> that JavaScript uses to construct new objects. To work around this, proxies of JavaScript classes within Python gain a <code>new()</code> which calls their constructor.</p>
<p>If you have a JavaScript class defined like so:</p>

```py
var Boat = class Boat{
    constructor(size, power){
        this.size = size
        this.power = power
    }
}
```

<p>We can construct new instances of the class within Python like so:</p>

```py
from js import Boat

sailboat = Boat.new("33ft", "sailpower")
tugboat = Boat.new("80ft", "diesel")

print(f"{sailboat.size=}, {tugboat.power=}")
```

<p>This also works for classes already defined in the JavaScript global scope. For example, to create a new JavaScript <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Float64Array">Float64Array</a> (an array of 8-byte floats), you can use the following similar syntax:</p>

```py
from js import Float64Array

my_array = Float64Array.new([1,2,3,4])
    
print(my_array)
print(f"{my_array.byteLength= }")
```