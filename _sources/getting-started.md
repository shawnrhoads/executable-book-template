# Getting Started

This Jupyter Book is a template for others to compile supplemental materials (e.g., code, visualizations) for their projects into their own Jupyter Book website.

If you use this template, please use the following citation:

<blockquote>Rhoads, S. A. (2021). Executable Book Template. Zenodo.</blockquote>
<br>

## How to use this template

[Click here](https://github.com/shawnrhoads/executable-book-template/generate) to generate a new GitHub repository based on this [template](https://github.com/shawnrhoads/executable-book-template). Alternatively, you can click "Use this template" on the repository page. This will allow you to create a new repository that mirrors the contents required for this Jupyter Book.

### Modifying files

In your new repository, you can modify, delete, or add any files with the following extensions: `*ipynb`, `*md`, `*csv`, `*pdf`. Note that only `*ipynb` and `*md` files will be used to generate your Jupyter Book, but `*csv` files may contain machine-readable data that are required to generate any outputs from your code. 

```{note} Important!
The following files are required to build the Jupyter Book and **should not** be deleted: `exec-book-template.yml`, `docs/_config.yml`, `docs/_toc.yml`, `.github/workflows/deploy-book.yml`. However, you can edit their contents relevant to your project. 
```

Here is a list of all files and descriptions included in this repository:

**Files required to build book**
- `.github/workflows/deploy-book.yml`: Text file containing the ingredients to run a [GitHub action](https://github.com/features/actions) that builds the Jupyter Book. This action will execute whenever you commit a change to the `main` branch.
- `exec-book-template.yml`: Text file containing all of the packages required to execute your `*ipynb` files. It is used to create an [Anaconda](https://www.anaconda.com/products/individual#Downloads) environment (i.e., using the following command: `conda env create -f exec-book-template.yml`). You can modify any channels or dependencies (and versions) to meet your needs. However, you will need to keep `pip` and `jupyter-book==0.10.2`. If you change the name of this file or environment, then you will also need to edit `.github/workflows/deploy-book.yml`. 
- `docs/_config.yml`: Text file containing the ingredients to build your Jupyter Book. See [this page](https://jupyterbook.org/customize/config.html) for more information.
- `docs/_toc.yml`: Text file containing the ingredients to build your Jupyter Book table of contents. See [this page](https://jupyterbook.org/structure/configure.html) for more information.

**Optional files**
- `LICENSE`: Text file containing the license for this template. You may [change this](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/licensing-a-repository#searching-github-by-license-type) to fit your project's needs.
- `README.md`: Markdown file that should be updated to reflect the contents of your project. This will automatically serve as the `getting-started` page for your Jupyter Book website. See built webpage [here](https://shawnrhoads.github.io/executable-book-template/getting-started.html). 
- `.gitignore`: Text file containing specific extensions that you want Git/GitHub to ignore.
- `docs/slides/*pdf`: Slides for Jupyter for Neuroimagers workshop.
- `docs/data/*csv`: Example comma-separated dataset.
- `docs/data/*nii.gz`: Example 3D neuroimaging data.
- `docs/index.md`: Markdown file that will be the homepage of the Jupyter Book that should contain a brief description and/or citation to your project. See built webpage [here](https://shawnrhoads.github.io/executable-book-template/).
- `docs/data.ipynb`: Example Jupyter Notebook file that contains some code for loading and displaying data from a `.csv` file and visualizations. See built webpage [here](https://shawnrhoads.github.io/executable-book-template/data.html).
- `docs/preproc.ipynb`: Example Jupyter Notebook file containing Markdown and non-executable code (e.g., `bash`). See built webpage [here](https://shawnrhoads.github.io/executable-book-template/preproc.html).
- `docs/study1.ipynb`: Example Jupyter Notebook file containing Python code for running analysis on behavioral data and plotting results. See built webpage [here](https://shawnrhoads.github.io/executable-book-template/study1.html).
- `docs/study2.ipynb`: Example Jupyter Notebook file containing non-executable code for neuroimaging analyses and Python code for plotting and reporting results. See built webpage [here](https://shawnrhoads.github.io/executable-book-template/study2.html).
- `docs/jupyter.ipynb`: Example Jupyter Notebook file highlighting some features of Markdown syntax. See built webpage [here](https://shawnrhoads.github.io/executable-book-template/jupyter.html).
- `docs/R.ipynb`: Example Jupyter Notebook file containing code for loading data from a `.csv` file and running an analysis in R. This will only work if `r` is listed as a channel and `r-irkernel` is listed as a dependency in `exec-book-template.yml`. See built webpage [here](https://shawnrhoads.github.io/executable-book-template/R.html).
- `docs/Python.ipynb`: Example Jupyter Notebook file containing code for loading data from a `.csv` file and running an analysis in Python. See built webpage [here](https://shawnrhoads.github.io/executable-book-template/Python.html). 

### Hosting your Jupyter Book

Once you have added, modified, or deleted any necessary files for your project, then you can publish it via GitHub Pages! To do this, go to your repository Settings > Pages, then make sure your "GitHub Pages site is currently being built from the `gh-pages` branch" and save.


## Other tips and tricks

- Please visit the [Jupyter Book](https://jupyterbook.org) for more ways to customize your Jupyter Book!
- [Here](https://jupyterbook.org/interactive/interactive.html) is some information regarding interactive data visualizations.
- This template uses the [Insipid Sphinx Theme](https://github.com/mgeier/insipid-sphinx-theme), but other themes can be found [here](https://sphinx-themes.org/). The [Sphinx Book Theme](https://sphinx-book-theme.readthedocs.io/en/latest/) is the default.
- Gain inspiration from other Jupyter Books [here](https://executablebooks.org/en/latest/gallery.html)!