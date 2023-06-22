Here is the rough vision of what the tutorial will look like. You can also find reference materials at [jsoma.github.io/quarto-tutorial](https://jsoma.github.io/quarto-tutorial)

## Setup 

- Install Quarto from [quarto.org](https://quarto.org)
- Install Visual Studio Code from [code.visualstudio.com](https://code.visualstudio.com/)
- You can install Python if you want, R if you want. I was having some Python trouble and installed [miniconda](https://docs.conda.io/en/latest/miniconda.html) and life worked great after that.

Finally, download [tutorial-content.zip](https://github.com/jsoma/quarto-tutorial/raw/main/tutorial-content.zip) and extract it on your machine.

## Rendering websites

Since it's based on [pandoc](https://pandoc.org/), Quarto can work with *almost any kind of file!*

### Jupyter notebooks

Most people are Python people, so we'll start with Jupyter notebooks

But it doesn't matter if you don't have Python or Jupyter installed.

Jupyter is a file format that looks like JSON, you can export as HTML, you could use `nbconvert` or something else. But it's not very customizable!

Pandoc can work with Jupyter notebooks, but again, not ideal interface, pretty confusing

Quarto makes it easy

Right-click `notebook.ipynb` in VS Code, "Open in Integrated Terminal," then run this code:

```bash
quarto render notebook.ipynb
```

It will automatically make an html file. It just takes all of the pre-rendered HTML - even if you don't have Jupyter or Python installed – and turns it into a file. Nice!

### Customizing the rendering

I don't like that it adds a little extra folder, I just one html file, so I usually use this command:

```bash
quarto render notebook.ipynb --to html --embed-resources
```

And there are all sorts of options you can add there, but it gets pretty painful pretty quickly, so it's better to actually add the options inside of the notebook instead of in the command-line command.

This is called YAML. First we'll add html/embed resources, then title, then linkcolor, then theme, then toc

```yaml
---
title: "This title goes at the top of the page"
format:
    html:
        toc: true
        embed-resources: true
        linkcolor: salmon
        theme: cosmo
---
```

You can export to all sorts of different formats, PDF, Word docs, reveal.js presentations, etc.

### Quarto Markdown

Now, people who are R people? Quarto allows you to use Jupyter notebooks but it really like this other thing called Quarto markdown, which is based on R markdown.

You can open `quarto-markdown.qmd` to edit, there should be little 'Render' button on the top right.

We'll slowly add [this code until it is complete](tutorial-content-after/quarto-markdown.qmd).

If you wanted to add R code, you can do that, too.

### Multi-page websites

I like Quarto best for managing multi-page websites, which means we don't want to use one single page with yaml. We create a new file, `_quarto.yml`, and use it to set up the site.

Let's add all of our pages to the site. Then we'll add our format content. Then `output-dir: docs` so it can go up on GitHub Pages.

The completed version will [look like this](tutorial-content-after/_quarto.yml).

```yaml
project:
    type: website
    output-dir: docs

format:
    html:
        toc: true
        linkcolor: red
        theme: cosmo

website:
    title: "Example Quarto website"
    sidebar:
        style: "docked"
        contents:
        - href: index.qmd
            text: Home
        - section: "Examples"
            contents:
            - text: "Jupyter notebook"
                url: notebook.ipynb
            - text: "Quarto Markdown"
                url: quarto-markdown.qmd
            - text: "Observable JS"
                url: observable.qmd
            - text: "Python + R"
                url: python-and-r.qmd
    page-footer: 
        border: false
        background: dark
        left: >
        ©2023, Jonathan Soma
        right: 
        - icon: github
            href: https://github.com/jsoma
        - icon: twitter 
            href: https://twitter.com/dangerscarf
        - icon: envelope
            href: mailto:jonathan.soma@gmail.com
``` 

### Python + R

To use Quarto to have Python and R talk to each other, we'll add the code in [this file](tutorial-content-after/python-and-r.qmd).

### Observable

Let's just run `quarto preview` for all of this. There's another file, called Observable JS. Let's go look at it.

Amazing!

## Publishing

Now let's get it on GitHub Pages. You can use `quarto publish` but I don't like it. _Leon_ likes it, but I'm pretty sure it caused problems for him the other day, so I'm in charge of not letting you use it.

1. Create a new repo on [GitHub](https://github.com/)
2. Add all of your files in, including your `docs` folder. You can even drag and drop!
3. Publish from the `docs` folder.

Done! You have a website!
