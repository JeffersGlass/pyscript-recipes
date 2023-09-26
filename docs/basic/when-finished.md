# Run Code when PyScript Has Finished

<p>The PyScript loading cycle does many things - loads plugins, instantiates the <code>&lt;py-script&gt;</code> and <code>&lt;py-repl&gt;</code> tags, attachs event listeners and so on. To cause something to happen once this entire process is complete, the easiest way is to use a <a href="https://docs.pyscript.net/latest/guides/custom-plugins.html">plugin</a>. Plugins can be written in Python or JavaScript; we'll show examples of both.</p>
<h3>JavaScript</h3>
<p>To run run some JavaScript code when PyScript completes, create a new <code>.js</code> file with a name of your choice. Here, we'll use <code>example.js</code>. In this file, add the following:</p>

```py
export default class ExamplePlugin { // the name of the class is unimportant
    afterStartup(interpreter){
        console.log("Hello, world!") // your code here 
    }
}
```

<p>Then add this file to the <code>plugins</code> list inside the <code>&lt;py-config&gt;</code> tag, like so:</p>

```py
<py-config>
    plugins = ['example.js']
</py-config>
```

<h3>Python</h3>
<p>To run run some Python code when PyScript completes, create a new <code>.py</code> file with a name of your choice. Here, we'll use <code>example.py</code>. In this file, add the following:</p>

```py
from pyscript import Plugin # A base class for plugins

class ExamplePlugin(Plugin): # The name of the class is unimportant
    def afterSetup(self, interpreter):
        print("Hello, world!")    

plugin = ExamplePlugin() # The object named 'plugin' will have its methods called
```

<h3>The <code>Interpreter</code> Argument</h3>
<p>In both cases, the <code>interpreter</code> argument is an <a href="https://github.com/pyscript/pyscript/blob/13e9252260c0b2c43c77e71deb4a5f0d0cada485/pyscriptjs/src/interpreter_client.ts#L13">interpreter_client</a> object, which wraps the actual interpreter. Key methods include <code>run()</code> for executing Python code. See the previous link for the source and details.</p>