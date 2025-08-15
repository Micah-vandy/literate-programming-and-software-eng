# Literate Programming with Python

> A session on literate programming with Python  
> Charreau Bell, PhD  
> 2025-08-14  

## Link Outline

* [Day 1 | Literate Programming](#resources-for-module-1-literate-programming--motivation)
* [Day 2 | Jupyter Notebooks: Single Source of Truth](#day-2-jupyter-notebooks-single-source-of-truth)

## Introduction

Literate programming is a programming paradigm that combines programming and documentation into a single, coherent document. It is a way to write code that is both easy to understand and easy to modify. In this session, we will explore why literate programming is useful, and how to use it with Python. We'll also explore some software design principles as we're writing code for packaging up for actual use.

## Notes and Caveats
- In this session, we will work *locally* on our own machines, using the software that we have installed, and using the ideas that have been taught previously in the bootcamp.
- This is a "put it all together" moment where things CAN and WILL go wrong, but luckily it's not during a class where you're being graded.

## Pre-Setup
In this workshop, I will be using Cursor which uses AI to help you write code. It is built on top of VSCode, so it will look SUPER similar to VSCode if you want to use that. You can uninstall Cursor later if you want to directly follow along.

1. Download Cursor from [here](https://cursor.com/downloads)
2. Install Extensions:
  - Python:
    - Python by ms-python
    - Python by Anysphere (Cursor-specific completions - when you go to VS Code you will install a different Python)
    - Python Debugger by ms-python
    - Black Formatter by ms-python (Suggested but optional)
3. Jupyter:
    - Jupyter by ms-toolsai
    - Jupyter Cell Tags
    - Jupyter Jupyter Notebook Renders
    - Jupyter PowerToys
    - Jupyter Slide Show
4. Quarto (by quarto)


## Resources for Module 1: Literate Programming | Motivation

### An update presentation for a supervisor
Link to update slides: [Lab Update](https://vanderbilt365-my.sharepoint.com/:b:/g/personal/charreau_s_bell_vanderbilt_edu/EYz8t6XYFBJIoayOklYn-5UBtobUXKHWyghHwBLboQTqQw?e=0DOWgA)

**Your task:** What questions would you have if you were the supervisor?
You can use generative AI to help you generate questions.

### Setup
1. Clone the repository in your local environment
2. Create a new environment (which environment will you use?)
  - Why do we use environments again?
```bash
# choose to make a python virtual environment
python -m venv venv
```
3. Activate the environment
```bash
# activate the environment
source venv/bin/activate
```
4. Install the dependencies
```bash 
pip install ipykernel pandas matplotlib seaborn scikit-learn nbdev
```
5. Open the notebook
6. Have fun!

## Resources for Module 2 | Literate Programming - Hands on
See above for installation instructions.
* We will use the notebook in the repo.

***

# Day 2: Jupyter Notebooks: Single Source of Truth
Today, we'll finish the topics from yesterday, extending specifically into using Jupyter Notebooks a multipurpose single source of truth. As we noted yesterday, with additional tooling, we're able to use Jupyter Notebooks for a lot more than just data analysis.
- Overview of content
- Style of final workshop? [TopHat Response](https://app.tophat.com/guest) **Code**: 763949

## Pre-Setup

* We will be using the same repo from yesterday, the same workspace, and the same environment, and now we need to do a new pull from our remote repository. **This is a new and common workflow, and here, we will encounter errors that we almost always encounter, especially if everyone works in the same files on the same branch.**

**Observations:**
1. **Unstaged, uncommitted changes:** We have changed a file locally, but haven't committed the changes. In this case, we also don't intend to commit the changes since we're pulling from a public repository we can't commit to.
2. **Untracked files we don't want to track:** We have tons of files in our git repository locally that git wants to track, because we don't want to because they don't need to be versioned.

**Solutions:**
1. **If we don't want to commit the changes but want to keep using the changes:** We can use `git stash` to stash the changes, and then `git pull` to pull the changes from the remote repository. If we want to restore the changes to our freshly pulled repository, we can use `git stash pop` to restore the changes from the stash.
2. **Files we don't want to track:** Create a `.gitignore` file in the root of the repository and add the files or directories we don't want to track. Usually, you **do** check a `.gitignore` file into the repository so that everyone can use it. Steps of creating a local `.gitignore` file:
  - Create a new file in the root of the repository called `.gitignore`
  - Add the files or directories we don't want to track. We'll add the following:
  ```
  .DS_Store
  .ipynb_checkpoints/
  venv/
  __pycache__/
  .env
  ```
Great! Now we're ready to start!

## Resources for Module 3 | Useful Jupyter Notebooks
* Lecture slides
* [TopHat Response](https://app.tophat.com/guest) **Code**: 763949
* 5 minute break

## Resources for Module 4 | Jupyter Notebooks: Single Source of Truth
* [**Main reference**: nbdev](https://nbdev.fast.ai/)

### Nbdev installation and setup notes for existing repositories
You'll do all of the following in your terminal.
1. Install the package (you probably already have, but if not):
```bash
pip install nbdev
```
2. Install **Quarto**. Yesterday, we talked about needing to install a Quarto executable. Nbdev has us covered. If you have questions about root access, nbdev, and quarto, see details [here](https://nbdev.fast.ai/getting_started.html#q-why-is-nbdev-asking-for-root-access-how-do-i-install-quarto-without-root-access).
```bash
nbdev_install_quarto
```
3. Add configuration settings for nbdev.
```bash
nbdev_new
```
This does a lot, but most importantly for an existing repository:
* Adds the `settings.ini` for settings for the module that will be built
* Adds on to your .gitignore files
* Adds a CI/CD pipeline through github actions to ensure the consistency of your codebase and automatically deploy your documentation
* Very rudely replaces your README

4. Add Pre-Commit Hooks
```bash
nbdev_install_hooks
```
This basically means that a few things are done automatically before you commit:
1. Removing execution counts and unneeded metadata (without removing cell outputs)
2. Standardizing whitespace

Generally, you will need to setup pre-commit hooks for this to work for VS Code or Cursor. You can do that following the instructions [here](https://nbdev.fast.ai/tutorials/pre_commit.html) so that they run automatically. **Today we're just going to skip this and do it manually, but this also means that you have to remember to run it manually until you create the pre-commit hooks.**

5. Building your library
```bash
nbdev_export
```
This creates modules from any notebooks in the specified directory. The directory is specified in the `settings.ini` file. Let's make a change to see the outcome of this action.

6. Building and previewing your documentation
```bash
nbdev_preview
```
This allows you to see your documentation in a browser started by Quarto. This is what will be shown on your GitHub Pages site.

### Best practices for actual analytical + production development
* `nbdev_clean` your notebooks before you add and commit them. Often it helps if you kill the kernel if you're pretty much done with that notebook, otherwise the kernel sometimes adds back in metadata that you don't want.
* `nbdev_prepare` your entire codebase before you add and commit them as well. This keeps your library in sync with your notebooks among the other great things about `nbdev_prepare`.

### Nbdev | Pitfalls and Caveats

* Nbdev was really created for software development in Jupyter notebooks because they deeply augment the ability to understand what's going on in software and why. The capacity of literate programming, even for software is dramatic.
* This means that they're following **software development principles** which means they have tons of tests, and they want them to run automatically. So **everytime you run `nbdev_prepare`, it's going to literally run all of your code.** You have to suppress this behavior by adding cells to do so. This looks like a yaml header that is a **raw cell**at the top of the notebook that looks like this:
```yaml
---
skip_exec: true
---
```

### Actually using the functionality for our purposes
#### Cell tags:
* `default_exp module_name` is the name that the cells will by default be exported to
* `#| export` is the tag that will indicate that we want this cell exported to the module
* `#| hide` is the tag that will indicate that we want this cell hidden from **the documentation**.

Let's try this.

### Your own repo on GitHub
Currently, you can't see any of this functionality is working because you can't commit to my repo. Instead, you will create a new repo and we'll use `nbdev_new` in it to create a fully new module.

### Create your own repo in which you will house this repository and initalize using `nbdev_new`
1. Go to [GitHub](https://github.com/) and create a new repository, making sure that you're logged in. Make sure that the repository is **public** for now. You can change this later.
2. Do not add a readme, .gitignore, or LICENSE file. This is so you can have a completely empty repository.
3. Observe the instructions on the resultant page but do nothing with this information for now. Just observe them.
4. Clone the repository to your local machine:
```
git clone <your-new-repo-url>
```
5. `cd` into the repository
6. Create a new environment and add nbdev and ipykernel
```
python -m venv venv
source venv/bin/activate
pip install nbdev ipykernel
```
6. `nbdev_new` to initialize the repository with nbdev.
7. Let's open in Cursor.

### Let's now push to your new repo
Now, we see the blandness of the empty repository.
It's now time to do all of the git-ly commands! Except we're going to also add in all the nbdev stuff.
1. Save all notebooks
2. `nbdev_prepare`
3. Git steps:
```
git add .
git commit -m "Uploading additional documentation to the repo."
git push -u origin main
```
4. `nbdev_export`
5. `nbdev_preview`

### Let's observe the behavior on GitHub.
* GitHub Actions
* New repo content

Currently, we can't see the documentation although we did push it to the repo. This is because we don't have GitHub Pages enabled. You can access the original instructions [here](https://nbdev.fast.ai/tutorials/tutorial.html#enable-github-pages) but the steps are reproduced below.
1. Go to the repository settings - the "Settings" tab in the top bar
2. Scroll down to the "Pages" section
3. Under **"Source"**, make sure **"Deploy from a branch"** is selected, then select the **"gh-pages"** branch
4. This will be automatically set up for you.
5. Visit your GitHub Pages site to see the documentation.

### Actually using the functionality to decrease notebook length
Now, let's explore reusabilility of content in notebooks. We will explore the `nbs/00_core.ipynb` notebook first and then move to create a new notebook which utilizes this functionality.

1. Install an editable version of the library so that you can actually access the library.
```bash
pip install -e '.[dev]'
```

2. Create a new notebook in the `nbs` directory called `01_analysis.ipynb`
3. Enable hot reloading of updated packages in your notebook.
```
%reload_ext autoreload
%autoreload 2
```
4. Import the `foo` function from the library and use it: `from demo_package.core import foo`
5. Run the `foo` function and add whatever else you like, including new analytical content.

**When you need to update source:**
1. Make a change to the `foo` function - have the foo function print the string "Ran the foo function".
2. Run the other notebook again and note the lack of update.
3. `nbdev_prepare` to rebuild the library.

## Things to Mentally Bookmark (Day 1)
* **Literate programming**: Stop copy/pasting and losing information in powerpoint presentations, particularly for weekly updates. Present from the Jupyter notebook or use tools that make the Jupyter notebook easier to present.
  * **Use Real Estate Wisely**: A Jupyter notebook has limited real estate so use it well. Explain and narrate your code. Remove unwanted outputs that make the Jupyter notebook long without adding value.
  * **Eat Food and Drink Water**: If you don't, you might pass out while you're teaching.
* **IDEs and Environments**:
  * **Extensions**: Add to VSCode (and Cursor) to provide additional tooling like Jupyter notebooks.
  * **Pip-style virtual environments**: Installs packages (or links to existing packages) in the current directory (or the specified directory). Pop ups will allow you to choose to use the environment for the entire directory/workspace for simplicity.
  * **Jupyter Notebook kernel**: The kernel has the Python version and packages, and usually this will be your venv or your conda environment.
  * **Jupyter Extension**: The Jupyter extension gives you the left sidebar to explore the **notebook outline** by headers. It also gives you access to API documentation for what's under the cursor in code cells. 

# Deepen Your Understanding
## Revise the Day 1 `literate_programming_starter` notebook
Currently, this notebook doesn't actually fully implement literate programming principles.

1. Tell the story of the analysis from beginning to end. Make sure that there is some sort of conclusion added for each meaningful part of the analysis; in other words, if there's table, say something about it. If there are plots, make some sort of meaningful conclusion. Make sure that unnecessary information is removed.
2. Implement some additional functionality that can leverage functionality from the first notebook in a second notebook of your creation. Use `nbdev` functionality to make this happen.

## Git Review
We had a bunch of interesting git moments with virtual environments, etc. Answer for your own benefit:
* What were some of the new commands that you learned and why did we use them?
* Compare and contrast conda environments and python environments. Why might you use one over the other?

## IDEs
We had a great time with Cursor. Describe to yourself the following:
* Why did we need to install extensions?
* What are the different panes of Cursor and how do we show/hide them?
* How do we access the terminal?
* How do we debug? Why do we debug?