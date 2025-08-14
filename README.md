# Literate Programming with Python

> A session on literate programming with Python  
> Charreau Bell, PhD  
> 2025-08-14  

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
