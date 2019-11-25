# Welcome to nbdev




`nbdev` is a library that allows you to fully develop a library in [jupyter notebooks](https://jupyter.org/), putting all your code, tests and documentation in one place. That is: you now have a true [literate programming](https://en.wikipedia.org/wiki/Literate_programming) environment, as envisioned by Donald Knuth back in 1983!

Using the interactive enviromnent, you can easily debug and refactor your code. Add `#export` flags to the cells that define the functions you want to include in your python modules:

![An exported cell](nbs/images/export_example.png)

Here the function `add_init` is defined in the first cell (marked with the export flag) and tested in the second cell.

Using notebooks written like this, `nbdev` can create and run any of the following with a single command:

- Searchable, hyperlinked documentation
- Python modules, following best practices such as automatically defining `__all__` ([more details](http://xion.io/post/code/python-all-wild-imports.html)) with your exported functions, classes, and variables
- Pip installers (uploaded to pypi for you)
- Tests (run in parallel)
- Navigate and edit your code in a standard text editor or IDE, and export any changes automatically back into your notebooks

Since you are in a notebook, you can also add charts, text, links, images, videos, etc, that will included automatically in the documentation of your library. The cells where your code is defined will be hidden and replaced by standardized documentation of your function, showing its name, arguments, docstring, and link to the source code on github. For instance, the cells above are converted to:

![doc example](nbs/images/doc_example.png)

See below for *Installing* and *Getting Started*. In the other pages of the documentation, you can get more details about:

- the [export](http://nbdev.fast.ai/export.html) functionality from jupyter noteboks to a python library
- the [cli](http://nbdev.fast.ai/cli.html) commands you can use with nbdev in a terminal
- how [export2html](http://nbdev.fast.ai/export2html.html) buils a documentation for your libary
- how [sync](http://nbdev.fast.ai/sync.html) can allow you to export back form the pyhton modules to the jupyter notebook
- how [test](http://nbdev.fast.ai/test.html) put in your notebooks can be run in parallel to export a CI from your notebooks

## Installing

nbdev is is on PyPI so you can just run:
``` 
pip install nbdev
```

For an [editable install](https://stackoverflow.com/questions/35064426/when-would-the-e-editable-option-be-useful-with-pip-install), use the following:
```
git clone https://github.com/fastai/nbdev
pip install -e nbdev
```

## Getting Started

To begin your own project, click here: [nbdev template](https://github.com/fastai/nbdev_template/generate). Fill in the requested info and click *Create repository from template*, and a new GitHub repo will be created for you.

Now, open your terminal, and clone the repo you just created.

Next, edit the `settings.ini` file. Note that it contains all the necessary information for when you'll be ready to package your libary, so you shouldn't need to change the `setup.py` file provided by the template. The basic structure (that can be personalized provided you change the relevant information in `settings.ini`) is that the root of the repo will contain your notebooks, along with a folder `docs` where the doc will be auto-generated that contains everything for a [jekyll](https://jekyllrb.com/)-powered website. Because [GitHub Pages supports Jekyll](https://help.github.com/en/github/working-with-github-pages/setting-up-a-github-pages-site-with-jekyll), you can host your site for free on GitHub without any additional setup.

Your `settings.ini` is where all parts of nbdev look for any required configuration information. Once you've edited it, run the command `nbdev_build_lib` (which is automatically installed for you when you install `nbdev`. You'll now find that you have a new directory, with the name of whatever you set `lib_name` to in `settings.ini`.

Now, run `jupyter notebook`, and click `00_core.ipynb`. This is where you'll create your first module! Create Jupyter cells as you would in any notebook. For any cells that you want to be included in your python module, type `#export` as the first line of the module.

In the last cell of your notebook, you can then run:
<div class="codecell" markdown="1">
<div class="input_area" markdown="1">

```python
from nbdev.export import *
notebook2script()
```

</div>
<div class="output_area" markdown="1">

    Converted 00_export.ipynb.
    Converted 01_sync.ipynb.
    Converted 02_showdoc.ipynb.
    Converted 03_export2html.ipynb.
    Converted 04_test.ipynb.
    Converted 05_cli.ipynb.
    Converted 99_index.ipynb.


</div>

</div>

Or in the command line, you can run:
``` bash
nbdev_build_lib
```
as long as you are somewhere in the folder where you are developing your library. Either of these will do the same thing: update your module to include all exported cells in your notebook.

To enable documentation in your GitHub repo, click 'Settings' on the main repo page, scroll down to 'GitHub Pages', and under 'Source' choose 'master branch /docs folder'. GitHub will then show you a link to your working documentation site.

Finally, edit `99_core.ipynb`. This will be converted into your projects *README* file, and will also be the index for your documentation. You can use the module you just exported in this library, which means you can show real working code, and actual outputs. Once you have everything as you want it, run `nbdev_build_docs` in the terminal. This will export HTML versions of your notebooks to the `docs` directory, and will create hyperlinks for any words in backticks (as long as they exist in your module). It will also create a menu for all notebooks you have created, and a table of contents for each.

## Contributing

If you want to contribute to `nbdev`, be sure to review the [contributions guidelines](https://github.com/fastai/nbdev/blob/master/CONTRIBUTING.md). This project adheres to fastai`s [code of condut](https://github.com/fastai/nbdev/blob/master/CODE-OF-CONDUCT.md). By participating, you are expected to uphold this code. In general, the fastai project strives to abide by generally accepted best practices in open-source software development.

Make sure you have the git hooks we use installed by running
```
nbdev_install_git_hooks
```
in the cloned repository folder. 

## Copyright

Copyright 2019 onwards, fast.ai, Inc. Licensed under the Apache License, Version 2.0 (the "License"); you may not use this project's files except in compliance with the License. A copy of the License is provided in the LICENSE file in this repository.
