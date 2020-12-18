# Project template

A simple template for research project repos. Also check out [data science and
reproducible science cookie
cutters](https://github.com/audreyr/cookiecutter#data-science).

## Installation

Run the following

    ./install.sh YOUR_PROJECT_REPO_FOLDER

This script creates the following folders and files. 

1. `libs` for a software library for the project.
1. `data` for datasets and scripts for downloading datasets.
1. `exps` for timestamped experiments.
1. `paper` for manuscripts.
1. `workflow` for workflow scripts.
1. `.gitignore` that lists temporary and binary files to ignore (LaTeX, Python, Jupyter, data files, etc. )

## Set up

### Anaconda

First create a virtual environment for the project.

    conda create -n project_env_name python=3.7
    conda activate project_env_name

Install `ipykernel` for Jupyter and `snakemake` for workflow management. 

    conda install ipykernel
    conda install -c bioconda -c conda-forge snakemake

Create a kernel for the virtual environment that you can use in Jupyter lab/notebook.

    python -m ipykernel install --user --name project_env_kernel_name

### Vim

Copy & paste to .vimrc
```vim
set ts=4
set sts=4
set sw=4
set autoindent
set smartindent
set smarttab
set expandtab
set nohlsearch
"set number
"
call plug#begin('~/.vim/plugged')
Plug 'nvie/vim-flake8'
Plug 'hynek/vim-python-pep8-indent'
Plug 'Townk/vim-autoclose'
Plug 'scrooloose/syntastic'
Plug 'ivan-krukov/vim-snakemake'
call plug#end()

" PyFlake Configuration
let g:PyFlakeOnWrite = 1
let g:PyFlakeCheckers = 'pep8,mccabe,pyflakes'
let g:PyFlakeDefaultComplexity=10

"
" Syntax for snakemake
"
au BufNewFile,BufRead Snakefile set syntax=snakemake
au BufNewFile,BufRead *.rules set syntax=snakemake
au BufNewFile,BufRead *.snakefile set syntax=snakemake
au BufNewFile,BufRead *.snake set syntax=snakemake
```

### Git pre-commit

```bash
conda install -c conda-forge pre-commit
pre-commit install
```
