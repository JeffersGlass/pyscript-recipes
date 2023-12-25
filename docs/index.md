# PyScript and Pyodide Recipes

This site contains a number of code snippets and guideines for accomplishing specific tasks with [PyScript](https://pyscript.net), [Pyodide](https://pyodide.org), and [Micropython](https://micropython.org/).

<h3>What are Pyodide, PyScript,and Micropython?</h3>
<p><b>PyScript</b> is an HTML-focused framework for utilizing WebAssembly-based Python runtimes in the browser. It adds additonal Python and HTML API's to ease integration of Python with web development.</p>
<p><b>Pyodide</b> is a distribution of Python for Web Browsers and NodeJS. It takes the CPython interpreter, compiles it to <a href="https://webassembly.org/">Web Assembly</a> (using <a href="https://emscripten.org/">Emscripten</a>), adds some additional useful <a href="https://pyodide.org/en/stable/usage/api/js-api.html">JavaScript APIs</a> and <a href="https://pyodide.org/en/stable/usage/api/python-api.html">Python APIs</a>, and makes it all available via a CDN. Additionally, the Pyodide project provides <a href="https://pyodide.org/en/stable/usage/packages-in-pyodide.html">over 100 packages</a> with their C/Rust/Fortran extensions pre-compiled to run on WebAssembly; these are made available through an additional built-in tool called <a href="https://micropip.pyodide.org/en/stable/project/api.html">Micropip</a>.</p>
<p><b>Micropython</b> is a reimplementation of Python, originally intended for microcontrollers, that emphasizes small code side and rapid execution. Its download size is less than 5% of that of Pyodide/CPython, however due to its different object model, it is not generally compatible with CPython packages that have extensions in C, Rust, FORTRAN, etc.</p>

<h3>What is a recipe?</h3>
<p>A recipe is short snippet of code intended to do one simple thing. It is different from an <i>example</i>, which might be a fully-realized page accomplishing some holistic task; and a <i>tutorial</i>, which gives an in-depth explanation of the full usage of a specific piece of functionality or API.</p>
<p>Some recipes are followed by <i>tutorials</i> explaning how they work.</p>