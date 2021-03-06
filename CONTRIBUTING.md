## How to get in touch?
We often hang out on [this Telegram chat](https://t.me/opensuse_docs), which by the way is bridged to the IRC `#docs:opensuse.org` and to `#docs` on [this Discord channel](https://discord.gg/opensuse).

## What does the reviewing process look like?
```
new document ------> review on structure and contents #1 ------> review on language, style and punctuation #1
                                                                                        |
                                                                                        |
marked "ready for release" <--- review on language #2 <--- review on contents #2  <------
```

## What preparation do I need?
It's is minimal. Take a look at the repo structure. Then move onto the next section.

### Repo structure
For your information:
```
...
Pipfile     # dependencies listed in pipenv format
requirements.txt    # dependencies listed in pip format (added for compatibility purposes)
project/    # where you run your mkdocs commands from (while the pipenv commands are to be run from the root directory)
    docs/   # contents files that mkdocs injects when building the website
    site/   # the source files of the generated website after each 'mkdocs build' command.
    ...
...
```
`.gitignore` should not let you commit any `build` directory. Please make sure that is the case.

## Building and serving the docs
You will need to test your changes. This means some groundwork:
* You can either install mkdocs from pip or from a virtual environment.
* It's highly recommended to use a virtual environment and not pip, so that the dependencies of this project won't mess with your system-wide python packages / modules. You still need to use pip to install pipenv though ;).
* Personnally I am using pipenv, which you install on openSUSE distributions with: `pip3 install --user pipenv`. Then you'll need to add `~/.local/bin` to your `PATH`. The best method for that depends on your shell:
    * for `bash` add `PATH=$PATH:/home/your-user-name/.local/bin` to `~/.profile`
    * for `fish` run the following command once from a fish shell: `set -Ua fish_user_paths /home/your-user-name/.local/bin`
    * for `zsh` add `export PATH=$PATH/home/your-user-name/.local/bin` to `.zshrc`

  Finally reload your shell (for `bash`: `source ~/.profile`). 

* Then 
    1. clone this repo where you want in your home folder
    2. `cd` to it and run `pipenv install` to install the dependencies, and then `pipenv shell` to run the environment. 
    3. finally `cd` to `project` and run you `mkdocs` and `mkdocs-versioning` commands from there, i.e. `mkdocs build` to generate the web content and `mkdocs serve` to serve it (by default at http://127.0.0.1:8000/) (replace `mkdocs` with `mkdocs-versioning` if you want to produce a multi-version build instead). The built-in dev-server allows you to preview your documentation as you're writing it. It will even auto-reload and refresh your browser whenever you save your changes.
* Available commands & documentation on mkdocs: https://www.mkdocs.org/

## What does the collaboration workflow look like?
If you are new to `git` and GitHub, you might be interested in https://jarv.is/notes/how-to-pull-request-fork-github/.

__Checklist before opening a Pull Request (PR)__:
* When doing `git checkout -b <meaningful name> <...>`, did you make sure that `meaningful name` satisfied the schema described under __Branches__ below? If not, you can still rename it using `git branch -m <new name that satsfies the schema> `.
* Have you followed the style guidelines below under __Style__?
* If you have added a new article:
  * did it land in `/project/docs`? If not, move it there.
  * have you added it to [table of contents](https://github.com/openSUSE/openSUSE-docs-revamped/blob/dev/ToC.md)? Just follow the examples already there. The urls look like `https://github.com/openSUSE/openSUSE-docs-revamped/blob/dev/<some file.md>`
* Have you tested your work? If not consider the __Building and serving the docs__ section above.
* Are you going to make your PR editabled for us? If you don't know how, you will have to check the `Allow edits from maintainers` checkbox on the Pull Request screen, in GitHub. Otherwise we won't be able to work with you on your PR.

## Branches
* The default branch -- the working branch -- is not `main` or `master` but `dev`. I will merge from one milestone to the other.
* 4 types of branch names, named after the type of commits you want to contribute. PRs should whenever possible concern just one type of commit.
  * `structure` (how the textual and multimedia contents breaks down into different parts)
  * `design` (web and non-web visuals)
  * `web-functions` (functionalities invoked from the web release of the docs)
  * `contents` (textual and multimedia contents)

## Style
_Structure_. Each document should start with an intro stating the end goal, the important presuppositions (typically about pre-requirements) that the document is making, and an outline of the main steps on the path to the goal.

_Technical jargon_. Important and unavoidable jargon should be defined (typically inlined, with info boxes). Overall the document should be understanble by a teenager (think secondary school textbook).

_Format_:
* reference points and path items in italics, ex: "_Settings_ > _Energy Saving_"
* action in bold, ex. "click __Yes__"
* code instructions part of a stepwise recipe between line breaks in code, ex. 
```
$ sudo zypper dup
```
* short snippets of code or not part of a stepwise recipe can be inlined as in "... run `sudo zypper dup` before anything else".
