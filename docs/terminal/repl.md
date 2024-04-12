# Interactive REPL

To activate an interactive "REPL" for Python or Micropython, add the following two lines of code to the code of the terminal script:

```py
<script type="py" terminal worker>
    import code
    code.interact()
</script>
```

!!! warning Worker Only Feature
    The interactive REPL is only accessible when the terminal's interpreter is running in a worker.