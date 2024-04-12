# Controlling the Terminal from PyScript

The [xtermjs](https://xtermjs.org/) which underlies a given PyScript terminal can be accessed directly via the `__terminal__` global name, when code is running in a terminal. This can be used to control the properties of the terminal to, say, change the numbers of columns and rows:

```py
<script type="py" terminal >
    __terminal__.resize(40, 6)
    print("Lorem ipsum dolor sit amet consectetur, adipisicing elit. ")
</script>
```