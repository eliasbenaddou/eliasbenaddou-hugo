---
title: "Setting up Python Projects with Pyenv & Poetry"
date: 2022-04-30T12:11:59+01:00
draft: false
slug: ""
tags: ["tutorial"]
image: "/img/snake.jpg"
summary: "The best way to setup your new python projects using Pyenv for version management and Poetry for dependency management."
---

## Managing Python versions with Pyenv 
---

There are several ways to install Python on your system and each come with their advantages and disadvantages. For example, a data scientist will benefit from the pre-installed packages like SciPy and Numpy from a quick Anaconda installation. For developers however, it's better to use tools that provide ease of switching between different versions of Python as your projects may require specific versions. These tools are:

- [Pyenv](https://github.com/pyenv/pyenv) - Python version management tool to manage multiple Python installations
- [Poetry](https://python-poetry.org) - Manages Python virtual environments and the project dependencies within

If you're on Mac you may have a default Python 2.7 aleady installed on your system (although Apple has finally come to removing it from macOS 12.3). If you have also installed other Python versions through Anaconda or from python.org, you'll never quite know for sure which Python interpreter is being used when you run commands in your terminal. 

<center>{{< figure src="/img/snake_original.JPG" width=500 caption="Photo of a snake I took in Vancouver Aquarium, Canada in 2015"  >}}</center>

<style> 
#rcorners1 {
  border-radius: 5px;
  background: #73AD21;
  padding: 10px;  
}
</style>


Pyenv solves this problem by managing your Python executables in a simple and elegant way and here's how to install it.

<details>
<summary>How does Pyenv work?</summary>
<br>
Pyenv inserts <b> $HOME/.pyenv/shims </b> at the beginning of <b> PATH </b> to intercept calls to Python. A 'shim' is a special executable that will redirect the call to a specific python version. There is an order to which the python version will be selected, depending on the configuration:  
<br>
<br>

1) <b>Shell</b>: The environment variable <b>PYENV_VERSION</b>. This can be set with the command <b> export PYENV_VERSION=<python_version> </b>

2) <b>Local</b>: This is set in a <b>.python_version</b> file which is generated using the command <b> pyenv local <python_version></b>. It will be searched recrusively from the current directory until it reaches the root directory.

3) <b>Global</b>: This can be generated with command <b>pyenv global <python_version> </b>.

4) <b>System</b>: When there is no configuration found, the python version will resort to a default one already installed on the operating system.
</details>

### Installing Pyenv
_Windows users can follow the instructions in the Github repo [here](https://github.com/pyenv/pyenv)_  
Mac (using Homebrew):
```terminal
brew update
brew install pyenv
```

Once installed, we can first see a list of all python executables, if they are already installed on your system. 

```terminal
pyenv versions
```

<div id="rcorners1" style="background-color: grey;">

system  
\* 3.8.10 (set by /Users/eliasbenaddouidrissi/.python-version)  
  3.9.1  
  3.9.2  
  3.9.4  
</div>
<br>

I already have multiple python versions installed on my system and the global python interpreter has been set to 3.8.10 as shown by the asterisk. This can be checked by running 

```terminal
python -V
```

<div id="rcorners1" style="background-color: grey;">

Python 3.8.10
</div>
<br>

Let's now list all the available python versions available to install

```terminal
pyenv install --list
```
<div id="rcorners1" style="background-color: grey;">

Available versions:  
  2.1.3  
  2.2.3  
  2.3.7  
  2.4.0  
  2.4.1  
  2.4.2  
  2.4.3  
  2.4.4  
  2.4.5  
...
  
  </div>
<br>

There are many to choose from, but we'll assume we have no python versions installed yet and choose 3.8.11 to install now

```terminal
pyenv install 3.8.11
```

Once instaled, if we then run 'pyenv versions' again, we'll see our new version in the list. It won't yet be active and to avoid any conflicts with default python installations you may already have, we will not change the global python interpreter and instead we will allocate our python versions per project.

## Managing dependencies with Poetry
---
<br> 

It's best practice to install dependencies per project to isolate the specific versions of each package and to prevent conflicts. Virtual environments are the best solution and we'll let Poetry manage this for us.

### Installing Poetry
---

Poetry is a tool for dependency management and packaging in Python. It allows you to declare the libraries your project depends on and will manage them for you. To install Poetry run the following command

Mac 
```terminal
curl -sSL https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py | python
```

Windows Powershell  
```terminal
(Invoke-WebRequest -Uri https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py -UseBasicParsing).Content | python -
```

To apply the installation to your current shell session, run

```terminal
source $HOME/.poetry/env
```

It can also be added to .bashrc or .zshrc files

```terminal
export PATH="$HOME/.poetry/bin:$PATH"
```

### Creating a new Poetry project
---

Poetry will create a new folder structure for you, so in your parent project directory run

```terminal
poetry new my_new_project
```

📦my_new_project  
 ┣ 📂my_new_project  
 ┃ ┗ 📜__init__.py  
 ┣ 📂tests  
 ┃ ┣ 📜__init__.py  
 ┃ ┗ 📜test_my_new_project.py  
 ┣ 📜README.rst  
 ┗ 📜pyproject.toml  


For this project, let's allocate the python version 3.8.11 we already downloaded before with Pyenv. We can use the 'local' command while in the root direcotry of the new project

```terminal
pyenv local 3.8.11
```

Running 'pyenv versions' from this location will now show Python 3.8.11 as the Python version marked with an asterisk to indicate it is active for this directory.

Our next task is to tell Poetry to use this new python we just allocated to this project directory. To do this, run

```terminal
poetry env use python
```

<div id="rcorners1" style="background-color: grey;">

Creating virtualenv my-new-project-pmkxjn9K-py3.8 in /Users/eliasbenaddouidrissi/Library/Caches/pypoetry/virtualenvs
Using virtualenv: /Users/eliasbenaddouidrissi/Library/Caches/pypoetry/virtualenvs/my-new-project-pmkxjn9K-py3.8
  
  </div>
<br>


<details>
<summary>How to configure Poetry to save virtual environments in the project root?</summary>
<br>

As shown in the output above, the virtual environments by default are store in ../Caches/pypoetry/virtualenvs. It may be better that each virtual environment is created inside the project root instead as this will allow editors like VSCode to automatically load the virtual environment. To change the configuration for poetry to do this, run  
<br>

```terminal
poetry config virtualenvs.in-project true
```
<br>

For more information on configuring Poetry, visit the [configuration section](https://python-poetry.org/docs/master/configuration/) in the documentation.

</details>

Poetry comes with commands to add or remove packages, update packages and more so you don't need to manually configure any files. In the snippet below, we will add the package FastAPI

```terminal
poetry add fastapi
```

<center>{{< figure src="/img/poetry_add.png" caption="Poetry will install all the dependencies for fastapi using the latest stable versions available"  >}}</center>

The pyproject.toml file will be updated automatically with information about dependencies. If you wish to install development packages, you can use the option --dev when adding the package, and these will be installed to a separate section in the pyproject.toml file

<center>{{< figure src="/img/pyproject.png" caption="The pyproject.toml file will update once the packages are installed"  >}}</center>

This covers the basics of setting up a new project with Pyenv and using Poetry to install your dependencies. For more information about the tools, check the websites linked at the top of this page for documentation.