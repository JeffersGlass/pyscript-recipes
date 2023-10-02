# Uploading Files

!!! warning "This page is about allowing end users to upload files"
    This page is about setting up an interface for <i>the users of your page</i> to upload files. To setup files to be loaded on page load in PyScript, use <a href="https://docs.pyscript.net/latest/reference/elements/py-config.html#a-name-fetch-fetch-a"><code>&lt;py-config&gt; [[fetch]]...</code></a>
!!! abstract ""
    <i>The PyScript and Pyodide versions of this tutorial are identical</i>


<h2>Purpose</h2>
<p>As front-end frameworks, it is often useful for users of PyScript or Pyodide to allow users to upload their own individual files to the web page for processing. These might be CSV or parquet files of data, images for processing, text files etc.</p>
<h2>Recipe</h2>
<p>First, we'll need to set up a <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/file">file upload element</a> to accept the user's uploaded file.</p>
```html
<label for="Upload a File"></label>
<input type="file" id="file-upload">
```
<p>Then, include the following code to allow the user to upload a file, and to do something with it once its uploaded. (Replace the <code>print</code> statement with the work you want to do.)</p>
```py
from js import document, window, Uint8Array
from pyodide.ffi.wrappers import add_event_listener
    
async def upload_file_and_show(e):
    file_list = e.target.files
    first_item = file_list.item(0)
    
    my_bytes: bytes = await get_bytes_from_file(first_item)
    print(my_bytes[:10]) # Do something with file contents
    
async def get_bytes_from_file(file):
    array_buf = await file.arrayBuffer()
    return array_buf.to_bytes()
    
add_event_listener(document.getElementById("file-upload"), "change", upload_file_and_show)

```

<h2>Tutorial</h2>
<p>Let's start our Python code from scratch, and see how we'd go about setting up a a function to handle the file upload once it's triggered. (We'll handle actually attaching this function to our file upload element in a moment.)</p>
```py
# import a couple of useful objects from the JavaScript global namespace
from js import document, window
    
# this function will receive an event object pointing to the HTML element
# we can read its FileList ('files') and get the first item in it (.item(0))
def upload_file_and_show(e):
    file_list = e.target.files
    first_item = file_list.item(0)

```
<p>Once we have a reference to the <a href="https://developer.mozilla.org/en-US/docs/Web/API/File">File object</a>, we can extract it's contents to work with. There a <a href="https://developer.mozilla.org/en-US/docs/Web/API/File#instance_methods">multiple ways</a> in which you can receive a file's contents; perhaps the most versatile is by receiving a raw Iterable of its bytes:</p>
```py
from js import document, window, Uint8Array

# Because retreiving of a file's ArrayBuffer is an asynchronous process,
# we need to make our function async
async def upload_file_and_show(e):
    file_list = e.target.files
    first_item = file_list.item(0)
    
    my_bytes: bytes = await get_bytes_from_file(first_item)

    # Do something with the bytes once we have them
    print(my_bytes[:10])
    
async def get_bytes_from_file(file):
    # Get the File object's arrayBuffer - just an ordered iterable of the bytes of the file
    # https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer
    array_buf = await file.arrayBuffer()
    
    # Use pyodide's ability to quickly copy the array buffer to a Python 'bytes' object
    # https://pyodide.org/en/stable/usage/api/python-api/ffi.html#pyodide.ffi.JsBuffer.to_bytes
    # https://docs.python.org/3/library/stdtypes.html#bytes-objects
    return array_buf.to_bytes()

```
<!-- FUTURE: @when decorator -->
<p>Finally, we'll wire up the HTML file upload element to the function we just wrote. There are multiple ways to do this, but the cleanest way currently is to use a function from the Pyodide Foreign Function interface called <code>add_event_listener</code>. This function takes a reference to an element on the page, the name of an <a href="https://developer.mozilla.org/en-US/docs/Web/API/Event">Event</a>, and the name of the function or Callable to use as the function handler.</p>

```py
from js import document, window, Uint8Array
from pyodide.ffi.wrappers import add_event_listener
    
async def upload_file_and_show(e):
    file_list = e.target.files
    first_item = file_list.item(0)
    
    my_bytes: bytes = await get_bytes_from_file(first_item)
    print(my_bytes[:10]) # Do something with file contents
    
async def get_bytes_from_file(file):
    array_buf = await file.arrayBuffer()
    return array_buf.to_bytes()
    
# Use pyodide's FFI to attach the function as an event listener for the file upload element
# https://pyodide.org/en/stable/usage/api/python-api/ffi.html#pyodide.ffi.wrappers.add_event_listener
add_event_listener(document.getElementById("file-upload"), "change", upload_file_and_show)

```
<hr>
<p>See also:
    <ul>
        <li><a href="/file-download">File Download</a></li>
    </ul>
</p>
<!-- 
    TODO: Add notes on other ways to transform the arraybuffer into an object 
    to_file(), etc
    https://pyodide.org/en/stable/usage/api/python-api/ffi.html#pyodide.ffi.JsBuffer
-->
