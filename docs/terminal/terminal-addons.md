# Terminal Addons

The xtermjs console that powers the PyScript terminal can make use of [a variety of addons](https://xtermjs.org/docs/guides/using-addons/) to add specific functionality. The [fit](https://github.com/xtermjs/xterm.js/tree/master/addons/addon-fit) and [web links](https://github.com/xtermjs/xterm.js/tree/master/addons/addon-web-links) addons are included out-of-the-box. To add an addon, grab the terminal object using the [`__terminal__` global name](terminal-attribute.md) and add a newly instatiated addon object to it. You can instantiate the addon via JavaScript, or using the [js-integration/js-modules.md](ESM Module Loader) functionality included with PyScript:

```py
<py-config>
    [js_modules.main]
    "https://cdn.jsdelivr.net/npm/@xterm/addon-web-links@0.11.0/+esm" = "weblinks"
</py-config>
<script type="py" terminal>
    from pyscript import js_modules

    addon = js_modules.weblinks.WebLinksAddon.new()
    __terminal__.loadAddon(addon)
    
    print("Check out https://google.com")
</script>
```