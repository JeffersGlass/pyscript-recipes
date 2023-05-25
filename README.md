# PyScript/Pyodide Recipes 

This is the source for [pyscript.recipes](https://pyscript.recipes), a site highlight short, drop-in code snippets for PyScript and Pyodide.

#Contributing

## What is a Recipe? 

A recipe is short snippet of code intended to do one simple thing. It is different from an *example*</i>*, which might be a fully-realized page accomplishing some holistic task; and a *tutorial*, which gives an in-depth explanation of the full usage of a specific piece of functionality or API.

## Building this Site

To build this site, you will need to install the [Hugo Static Site Generator](https://gohugo.io/installation/) on your system. (While hugo has some npm wrappers, the native installations seem to be more errorproof). 

You will also need [npm installed](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm).

Once Hugo is installed, clone this repository and, from the root directory, run `npm install`.

When npm finishes installing all its packages, you can run `hugo server` from the root directory to see a live preview of the site, or `hugo build` to build a static copy.

## Submitting a PR

The site itself is built from source in a GitHub action when there is a merge to the main branch; you don't need to build/upload a static copy.

Please ensure your idea is, at its core a *recipe*; if there are additional clarifying details, consider adding a **tutorial** section *following* your recipe, so interested readers can learn more. See the [File Download](https://pyscript.recipes/basic/file-download) page for an example of this.

### Content Organization / Page Formatting

All pages in the `basic` section are, by default, formatted with a set of tabs across the top of the page for PyScript, Pyodide, and Micropython.

Each page has a section of text at the top that is common to the recipes for both PyScript and Pyodide. This is content is in `index.html`. The pyscript-specific content is in `pyscript.html` and the pyodide-specific content is in `pyodide.html`. If both tutorials are identical, you can place the content in a file called `both.html`, and the content will be duplicated to both tabs.

For instanance, to create two new recipes, one which has different content for PyScript and Pyodide and one which has identical content, their file structures might be:

```
└── content/
    └── basic/
        ├── my-new-post/
        │   ├── index.html
        │   ├── pyscript.html
        │   └── pyodide.html
        └── my-universal-post/
            ├── index.html
            └── both.html
```

### Index.html

Each `index.html` file should contain some [front matter](https://gohugo.io/content-management/front-matter/) which defines the page's Title (as displayed), its template (usually 'basic'), and its order on the sidebar ('weight'):

#### Index.html
```
---
Title: "File Download"
flavor: 'basic'
weight: 5
---
This is the first sentence of content for this recipe
```

### Other .html Files

Files `pyscript.html`, `pyodide.html`, and `both.html`, when the exist, ***must*** include some front matter so that Hugo will recognize and parse them. This can be empty frontmatter:

#### pyscript.html
```
---
---
This is the first sentence in the pyscript-specific part of this recipe
```

### Highlight shortcodes

Hugo includes simple access to source code highlighting via chroma, in the form of a template shortcode. For style reasons, highlight tags should be wrapped in an additional div with formatting, like so:
```html
<div class="code-wrapper" style="overflow-x: auto; ">
    {{< highlight python "linenos=True,hl_lines=3 22">}}
        print("Hello, world") #Your source here
    {{< /highlight >}}
</div>
```

The first argument to the highlight shortcore is the language to be highlighted. The second argument takes [a variety of options](https://gohugo.io/content-management/syntax-highlighting/#highlight-shortcode) as a comma-separated string, for managing things like line numbers and line highlights. If you don't need/want any of these options, the second argument should be an empty string (`""`).