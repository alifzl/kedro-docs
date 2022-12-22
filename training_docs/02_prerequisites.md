# Training prerequisites
## Operating system
Kedro supports macOS, Linux and Windows (8/10/11 and Windows Server 2016+). 

## Command line
You will need to use the command line interface, or CLI, which is a text-based application to view, navigate and manipulate files on your computer. 
    
## Python
Kedro supports [Python 3.7+.](https://www.python.org/downloads/) so you should make sure that it is installed on your laptop. 

We recommend using [Anaconda](https://www.anaconda.com/download) (Python 3.7 version) to install Python packages. You can also use `conda`, which comes with Anaconda, as a virtual environment manager when you install Kedro.

## Installing Kedro

### Using Anaconda/Conda/Miniconda

1. Create a virtual environment:

    `conda create --name kedro-trumpet python=3.10 -y`

2. Activate it:

    `conda activate kedro-trumpet`

3. Install Requirements
    `python  -m pip install --upgrade pip`

    `pip install -e src/requrements.txt` (it would take a while to complete, be patient :)) )

4. Install Kedro:

    `pip install kedro`

5. Make sure that the Logo comes up properly!

    `kedro info`


### Using virtualenv

    python -m venv .venv
    source ./.venv/bin/activate
    python  -m pip install --upgrade pip
    pip install -e src/requrements.txt
    pip install -e src
    kedro info


## Kedro training code
Download the [Kedro training repository](https://git.mielse.com).


## Git (optional)

Git is a version control system that records changes to files as you work on them. Git is especially helpful for software developers as it allows changes to be tracked (including who and when) across a project.

When you [download `git`](https://git-scm.com/downloads), be sure to choose the correct version for your operating system:


## Checklist
Please use this checklist to make sure you have everything necessary to participate in the Kedro training.

- [ ] You have [Python 3.7+](https://www.python.org/downloads/) installed on your laptop

- [ ] You have Anaconda or an alternative [virtual environment manager](https://www.anaconda.com/products/distribution) virtual environment manager

- [ ] You have installed [Kedro](#kedro)

- [ ] You have [downloaded the `trumpet-data-science-template` repository](#kedro-training-code) 

- [ ] You have [a code editor](#code-editor) installed for writing Python code

- [ ] You have a [command line](#command-line) installed


If you are able to complete all of the above, you are ready for the training! 

>**Note**: If you have any problems or questions in any of the above checklist, please contact a.fazeli@sheypoor.com and resolve the issues before the training.


_[Go to the next page](./03_new_project.md)_

