# The Py-Terminal

Users can add an interactive terminal to their page by adding `<script type="py" terminal></script>` (or `<script type="mpy" terminal>`). This initializes a terminal emulated powered by [xtermjs](https://xtermjs.org/) at that location on the page, which supports colors, formatting, and terminal control messages, allowing Python programs that expect to output to a rich console to display properly.

The `terminal` attribute can be combined with the `worker` attribute to create a terminal process whose code executes in a worker process, so that the main thread is not locked up.

```py
<py-config>
    packages = ['colorama']
</py-config>
<script type="py" terminal>
    from colorama import Fore, Back, Style
    print(Fore.RED + 'some red text')
    print(Back.GREEN + 'and with a green background')
    print(Style.DIM + 'and in dim text')
    print(Style.RESET_ALL)
    print('back to normal now')
</script>
```
