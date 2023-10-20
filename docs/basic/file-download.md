# Downloading Files

!!! abstract ""
    <i>The PyScript and Pyodide versions of this recipe are identical. This recipe does not currently work with Micropython, due to limitations in passing objects between JavaScript and Python.</i>
    
<h2>Purpose</h2>
<p>Many users user PyScript or Pyodide to create new files, or modify existing or uploaded files. One way to persist these files after the webpage is closed is to allow the user to download them.</p>
<h2>Recipe</h2>
<p>First, we'll need a button, link, or other element for the user to interact with to start the download. There are some actions (like file downloads) that web browsers will only permit in response to user actions; thankfully, downloading a file is one of that. You wouldn't want any arbitrary website to start downloading a file without your permission, right?</p>
```html
<button id="download">Click to Download</button>
```
<p>Then, include the following code to cause a text file to be created and donloaded when this button is clicked. The information in the <code>data</code> variable will be included in the fie; the filename of the file will be, in this example, <code>my_other_file_name.txt</code>,</p>

```py
from js import Uint8Array, File, URL, document
import io
from pyodide.ffi.wrappers import add_event_listener

data = "Hello world, this is some text."

def downloadFile(*args):
    encoded_data = data.encode('utf-8')
    my_stream = io.BytesIO(encoded_data)

    js_array = Uint8Array.new(len(encoded_data))
    js_array.assign(my_stream.getbuffer())

    file = File.new([js_array], "unused_file_name.txt", {type: "text/plain"})
    url = URL.createObjectURL(file)

    hidden_link = document.createElement("a")
    hidden_link.setAttribute("download", "my_other_file_name.txt")
    hidden_link.setAttribute("href", url)
    hidden_link.click()
    
add_event_listener(document.getElementById("download"), "click", downloadFile)
```

<h2>Tutorial</h2>
<p>Next, we'll start setting up a function that will be called to download our file. (We'll handle actually attaching this function to our file download button in a moment.)</p>
<p>Wiring up this function as an event listener means it will be passed an <a href="https://developer.mozilla.org/en-US/docs/Web/API/Event">Event Object</a>, but for our current example, we won't actually need it. We'll add <code>*args</code> to our function paramters to capture and swallow this argument.</p>

```py
import io

def downloadFile(*args):
    # The data we ultimately want to have in our file
    data = "Hello world, this is some text."

    #Transform our string of data into bytes; you may want to adjust the encoding here
    encoded_data = data.encode('utf-8')

    # convert data into bytesIO object which can be read as a buffer
    my_stream = io.BytesIO(encoded_data)
```

<p>Next we'll directly createa a new <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint8Array"><code>Uint8Array</code></a> in JavaScript which will hold our data; we'll pass it the size of our data in bytes so that its initialized to the correct size. Then, we can use the <a href="https://pyodide.org/en/stable/usage/api/python-api/ffi.html#pyodide.ffi.JsBuffer.assign"><code>assign</code></a> method from Pyodide's Foreign Function Interface to directly copy from the buffer of our BytesIO objec to the buffer of the Uint8Array object:</p>

```py
from js import Uint8Array
import io

def downloadFile(*args):
    data = "Hello world, this is some text."
    encoded_data = data.encode('utf-8')
    my_stream = io.BytesIO(encoded_data)

    #initialize the JavaScript array of Bytes with the right size
    js_array = Uint8Array.new(len(encoded_data))

    # Copy of the contents of the Python butter into the JavaScript buffer
    js_array.assign(my_stream.getbuffer())
```

<p>Once we have our data in a JavaScript buffer, we can create a new <a href="https://developer.mozilla.org/en-US/docs/Web/API/File">File</a> object so that the browser can treat our data as a file and download it:</p>

```py
from js import Uint8Array, File, URL
import io

def downloadFile(*args):
    data = "Hello world, this is some text."
    encoded_data = data.encode('utf-8')
    my_stream = io.BytesIO(encoded_data)

    js_array = Uint8Array.new(len(encoded_data))
    js_array.assign(my_stream.getbuffer())

    # File constructor takes a buffer, a name, and a MIME type. The name will not actually be used
    # https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types
    file = File.new([js_array], "unused_file_name.txt", {type: "text/plain"})
    url = URL.createObjectURL(file)
```

<p>Now that we have a File to work with, and an internal URL that the browser can point to, we'll create a "hidden" link to actually download this file. The link is hidden in that we don't actually ever need to add it to the page - simply creating the link object and telling the browser to "click" it is enough:</p>

```py
from js import Uint8Array, File, URL, document
import io

def downloadFile(*args):
    data = "Hello world, this is some text."
    encoded_data = data.encode('utf-8')
    my_stream = io.BytesIO(encoded_data)

    js_array = Uint8Array.new(len(encoded_data))
    js_array.assign(my_stream.getbuffer())

    file = File.new([js_array], "unused_file_name.txt", {type: "text/plain"})
    url = URL.createObjectURL(file)

    hidden_link = document.createElement("a")
    # The second parameter here is the actual name of the file that will appear in the user's file system
    hidden_link.setAttribute("download", "my_other_file_name.txt")
    hidden_link.setAttribute("href", url)
    hidden_link.click()
```

<p>Finally, we'll wire up our button to call our handler function. There are multiple ways to do this, but the cleanest way currently is to use a function from the Pyodide Foreign Function interface called <code>add_event_listener</code>. This function takes a reference to an element on the page, the name of an <a href="https://developer.mozilla.org/en-US/docs/Web/API/Event">Event</a>, and the name of the function or Callable to use as the function handler.</p>

```py
from js import Uint8Array, File, URL, document
import iobutt
from pyodide.ffi.wrappers import add_event_listener

def downloadFile(*args):
    data = "Hello world, this is some text."
    encoded_data = data.encode('utf-8')
    my_stream = io.BytesIO(encoded_data)

    js_array = Uint8Array.new(len(encoded_data))
    js_array.assign(my_stream.getbuffer())

    file = File.new([js_array], "unused_file_name.txt", {type: "text/plain"})
    url = URL.createObjectURL(file)

    hidden_link = document.createElement("a")
    hidden_link.setAttribute("download", "my_other_file_name.txt")
    hidden_link.setAttribute("href", url)
    hidden_link.click()
    
add_event_listener(document.getElementById("download"), "click", downloadFile)
```