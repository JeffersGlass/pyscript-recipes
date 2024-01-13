# Installing Python Packages

<p>In addition to <a href="https://pyodide.org/en/stable/usage/wasm-constraints.html#python-standard-library">most of the Standard Library</a>, many other Python pacakges can loaded and used in the Browser. There are three types of Packages that can be loaded:</p>
<ul>
    <li>Packages that have been <a href="https://pyodide.org/en/stable/usage/packages-in-pyodide.html">pre-built by the Pyodide team</a>, with their C/Rust/Fortran extensions pre-compiled to work in Web Assembly.</li>
    <li>Pure Python packages that are available on <a href="https://pypi.org/">PyPI</a>; that is, packages which publish a wheel ending in <code>-none-any.whl</code>. (<i>Some packages written only in Python do not publish Pure Python wheels; check the 'Download Files' section on PyPI to confirm.</i>)</li>
    <li>Pure Python wheels that you build yourself.</li>
</ul>

=== "PyScript (Pyodide)"

    <p>To install a new Python package in PyScript, include the name of the package or the URL of the self-built wheel in the `packages` list in code `<py-config>`</p>
    ```html
    <py-config>
        packages = ['astropy', 'pyyaml', 'https://example.com/files/someWheel-py3-none-any.whl']
        # packages can be from PyPI, Pyodide Packages, or self-built wheels
    </py-config>
    ```

=== "PyScript (Micropython)"

    !!! info
        It is not currently possible to install external modules for MicroPython. See the relevant issues on GitHub for [PolyScript](https://github.com/pyscript/polyscript/issues/62) and [MicroPython](https://github.com/pyscript/polyscript/pull/63).

=== "Pyodide"

    <p>To install a new Python package from PyPI in Pyodide, first install the <code>micropip</code> python package, then use <code>micropip.install(package_name)</code>. For example, to load the Pure Python package <code>pyyaml</code>, and use it in some Python code:</p>
    ```js
    async function main() {
        let pyodide = await loadPyodide(); //load pyodide

        await pyodide.loadPackage("micropip");
        const micropip = pyodide.pyimport("micropip");
        await micropip.install('pyyaml');

        // Once installed, packages can be imported and used
        pyodide.runPython(`
            import yaml
            document = """
            a: 1
            b:
                c: 3
                d: 4
            """
            y = yaml.safe_load(document)
            print(yaml.dump(y))
        `)
        };
    main();
    ```
    <p>To load a package built by the Pyodide project, use <code>pyodide.loadPackage</code>:</p>
    ```js
        //...
        await pyodide.loadPackage("astropy");
        //...
    ```
    </div>