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

## How we work: agents and students

Experiments are run in two tracks on the same repository and the same data.

| | Agent track | Student track |
|---|---|---|
| Who | the experiment agents on aster (worker + reviewer) | you, in your own clone |
| Start | write an Issue that meets `criteria.md` (use the Issue form), add the label `ready` | `git switch -c <any-name>` in your clone |
| Branch | `issue-N` (created by the dispatcher) | any name that is not `master` or `issue-N` |
| Code and small results | `exps/<date>_issue-N_<topic>/` | `exps/<date>_<topic>/` |
| Large outputs | `data/exps/<same folder name>/` | `data/exps/<same folder name>/` |
| Back to `master` | a person reads the result and merges | open a pull request; a person merges |

Rules:

1. **Code and results of an experiment live in `exps/<folder>/`; its large outputs live in `data/exps/<same folder name>/`.** The two names are identical so you can find one from the other. No person's name goes into a path: the file owner shows with `ls -l`, the author with `git log`. If the folder name already exists, add `-2`, `-3`, ...
2. **`data/raw/` is read only** (links to shared datasets). **`data/derived/` belongs to the main workflow** (`workflow/`); experiments write to `data/exps/`. When an experiment is worth keeping, a person moves it into the main workflow and its outputs into `data/derived/`.
3. **Never push to `master` directly.** Agents push to `issue-N`, students to their own branches, and a person merges after reading the result.
4. **GPUs are your call.** Say in the Issue (Compute) or in your own run what you need. On aster, GPU 0 and 1 are for experiments, 2 and 3 are shared with the student LLM service: check `nvidia-smi`, always set `CUDA_VISIBLE_DEVICES`, never use a GPU that is busy. Jobs over 2 GPUs or many hours belong on Spiedie.
5. **Do not write to `/data/datasets`.**

### Student quick start (on aster)

    git clone https://github.com/contexturelab/<repo>.git
    cd <repo>
    pixi install
    git switch -c my-topic

`data/` is already a symlink to the project's shared data directory, so it works right after the clone. Run with `pixi run ...`. See the Issues of the repo for what the agents are doing or have done: label `running` (working), `done` (reviewed), `needs-human` (waiting for a person).

### Ask the agents to run an experiment

Write the plan as an Issue with the form `Experiment plan` (every section filled in, see `criteria.md`), then add `ready`. To ask for a change after a run, comment on the Issue and add `ready` again. A new question or different data is a new Issue.

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
