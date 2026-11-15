# Project template

A simple template for research project repos, managed with [pixi](https://pixi.sh).

## Create a project

Click **Use this template** on GitHub, or run

    gh repo create YOUR_PROJECT --template skojaku/project-template --clone

Then rename the placeholder package `libs/project_package_name` (folder, `pyproject.toml`, and the entry under `[pypi-dependencies]` in `pixi.toml`) and rename the workspace in `pixi.toml`.

## Folders

1. `libs` for a software library for the project.
1. `data` for datasets and scripts for downloading datasets.
1. `exps` for timestamped experiments.
1. `paper` for manuscripts.
1. `workflow` for workflow scripts.
1. `.gitignore` that lists temporary and binary files to ignore (LaTeX, Python, Jupyter, data files, etc. )

## Set up

Install [pixi](https://pixi.sh), then in the project folder

    pixi install

This creates `.pixi/` (the environment, not tracked by git) from `pixi.toml` and pins exact versions in `pixi.lock` (tracked by git). Anyone who clones the repo gets the same environment with `pixi install --locked`.

Use the environment:

    pixi run snakemake -c 4      # run the workflow
    pixi run python script.py    # run anything inside the environment
    pixi shell                   # or open a shell in the environment

Add packages with `pixi add PACKAGE` (conda-forge or bioconda; preferred) or `pixi add --pypi PACKAGE` (only if it is not on conda). Commit `pixi.toml` and `pixi.lock` together.

For Jupyter, register the kernel once: `pixi run python -m ipykernel install --user --name project_env_kernel_name`. For notebooks, [marimo](https://marimo.io/) is preferred: `pixi run marimo edit`.

### Workflow config

    cp workflow/config.template.yaml workflow/config.yaml

and edit the paths. `workflow/config.yaml` is not tracked by git.

### Snakemake profile

    mkdir -p ~/.config/snakemake/default

and create `~/.config/snakemake/default/config.yaml`:

```yaml
# non-slurm profile defaults
keep-going: True
rerun-triggers: mtime
```

and add the following to `.zshrc` or `.bashrc`:

```bash
export SNAKEMAKE_PROFILE=default
```

## Agent skills

Skill files are not kept in this repo. Install the following skills from my GitHub repositories with [`npx skills`](https://github.com/vercel-labs/skills):

| Skill | Install |
|---|---|
| Snakemake style guide | `npx skills add skojaku/snakemake-skill --all` |

This list will grow as I add more skills.
