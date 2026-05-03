# Commands Dossier

A personal log of Git, GitHub, Python, Jupyter, and conda commands —
organised by *patterns*, not just lists. Built up gradually as I learn.

*Maintained by Isht Vibhu. Started 30 April 2026.*
*Add new entries as you learn them. Patterns over lists.*

---

## Guiding Principle

The first word on a command line is the name of a program.
Everything after it is instructions to that program.

- `python ...` → Python is running.
- `jupyter ...` → Jupyter is running.
- `git ...` → Git is running.
- `conda ...` → conda is running.
- `pip ...` → pip is running.

When confused, ask the program itself for help: `<program> --help`.
For subcommands: `<program> <subcommand> --help`.

---

## Pattern: short flags vs long flags

- `-X` → one letter, "short flag" (Unix tradition, fast typing).
- `--word` → full word, "long flag" (clearer, came later).

Most programs accept both forms for the same option.
Example: `git commit -m "msg"` and `git commit --message "msg"` are identical.

---

## Pattern: `python -m <module>`

Run any Python module as if it were a standalone command.
Used when a package provides a command-line entry point.

Examples:
- `python -m pip install <package>` — run pip via Python.
- `python -m venv myenv` — create a virtual environment.
- `python -m ipykernel install --user --name X` — register a kernel.
- `python -m http.server 8000` — start a quick web server.

---

## Pattern: "install" means different things

- `pip install <pkg>` — download a package from PyPI.
- `conda install <pkg>` — download a package from Anaconda's channel.
- `python -m ipykernel install ...` — *register* an existing thing.
  Nothing is downloaded here; just an entry is added to a list.

Read the context. The word "install" is overloaded.

---

## Git: local workflow

Set up once per machine:

```
git config --global user.name "Isht Vibhu"
git config --global user.email "ishtvibhu@gmail.com"
git config --global init.defaultBranch main
```

Inside any project folder:

```
git init                       # turn folder into a Git repository
git status                     # what has changed?
git diff                       # show me the actual changes
git add <file>                 # stage a file for the next snapshot
git add *.ipynb                # stage all notebooks
git commit -m "message"        # take the snapshot
git log                        # show the history
git log --oneline              # one-line summary per commit
git branch                     # which branch am I on?
git branch -m main             # rename current branch to main
```

---

## Git: working with GitHub

```
git clone <url>                # download a complete copy of a repo
git remote -v                  # which GitHub URL is this repo linked to?
git push                       # send local commits up to GitHub
git pull                       # pull latest changes from GitHub
git checkout <branch>          # switch to a branch
git branch -a                  # show all branches, local and remote
```

First push from a fresh repo sometimes needs:

```
git push -u origin main        # set 'origin/main' as default upstream
```

---

## conda: environments

```
conda create -n <name> python=3.11    # make a new environment
conda activate <name>                 # switch into it
conda deactivate                      # leave it
conda env list                        # list all environments
conda list                            # list packages in current environment
conda install <package>               # install via conda channel
conda remove -n <name> --all          # delete an environment entirely
```

---

## Jupyter: kernel management

After creating a new conda environment, register it as a Jupyter kernel:

```
conda activate <env-name>
pip install ipykernel
python -m ipykernel install --user --name <env-name> --display-name "Python (<env-name>)"
```

Then in Jupyter, refresh the page; the new kernel appears in the "New" menu.

To list or remove kernels:

```
jupyter kernelspec list                # show all registered kernels
jupyter kernelspec uninstall <name>    # remove one
```

A conda *environment* is a folder with its own Python and packages.
A Jupyter *kernel* is a registered entry that points at one such Python.
They are not the same thing — registration is a separate step.

---

## PowerShell helpers (Windows)

```
cd <folder>                    # change directory
cd ..                          # go up one level
dir                            # list folder contents (ls on Linux)
mkdir <folder>                 # make a new folder
copy <src> <dst>               # copy a file
move <src> <dst>               # move a file
type <file>                    # show file contents (cat on Linux)
echo "text" > file.txt         # write text to a file (overwrites!)
echo "text" >> file.txt        # append text to a file
```

To find files anywhere on disk:

```
Get-ChildItem -Path C:\ -Filter *.ipynb -Recurse -ErrorAction SilentlyContinue
```

---

## Concepts to remember

- A Git repository is just a folder with a hidden `.git` database inside.
- A commit is a snapshot. A branch is a named line of commits.
  `main` is the default branch. `HEAD` is "where I am right now."
- A pull request on GitHub is a polite proposal to merge a branch into another.
- Private GitHub repos return 404, not 403, when accessed without auth.
  GitHub will not even confirm such a repo exists.

---

## Lessons learned the hard way

- Never paste a long URL into a Jupyter notebook badge cell — line wraps
  break the JSON. Keep the URL on one line.
- Always run `git pull` before starting work if you sometimes edit files
  in the GitHub web interface. Otherwise the local copy goes stale.
- Spaces in folder paths (e.g. `C:\iv Asus Fx505dt\...`) work but require
  quotes when typed explicitly into commands.
- The credential helper `manager` (Git Credential Manager) handles GitHub
  authentication via browser — pick that, tick "always use."

---

## Adding new entries

When something new is learned, add it under the right section above —
or start a new section. Follow the same style:

- Show the command in a code block.
- Add a short comment after each command saying what it does.
- If a *pattern* is being noticed (something that repeats across tools),
  give it its own "Pattern:" subsection.

Patterns are more valuable than commands. The brain remembers ten
patterns more easily than a hundred commands.
