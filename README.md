# Development Environment Setup Guide

This is a brief guide for how to set up your machine for doing routine data science
projects and for developing python packages.

There are other ways to accomplish the same or similar, but this should ensure a clean
installation that is easy to update.

Some of it is to taste, but in generel the choices presented here are made with best
practices, sensible defaults and popularity in mind.

This guide is assuming a M-based Mac but should work with Intel macs as well.


## Getting everything in place

### 1. Install Homebrew

Homebrew is a package manager for macOS.  

Run the following command in your command line:
```bash
/bin/bash -c "$(curl -fsSL \
  https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### 2. Install iTerm2 (optional)

iTerm2 is an alternative to Terminal that is highly customizable and has additional
features.

Run the following command in your command line:
```bash
brew install --cask iterm2
```


### 3. Install Oh My Zsh (optional)

Oh My Zsh is framework for expanding the Zsh with helpful themes and plugins.

Run the following command in your Terminal:
```bash
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

Updates are installed by running:
```bash
omz update
```


#### 3a. Install Powerlevel10k theme

Run the following command in your Terminal:
```bash
brew install romkatv/powerlevel10k/powerlevel10k
echo "source $(brew --prefix)/opt/powerlevel10k/powerlevel10k.zsh-theme" >>~/.zshrc
```

Next run the following to restart your shell:
```bash
exec zsh
```

You will now be prompted to configure your powerlevel10k installation.

The configuration wizard can be re-run with:
```bash
p10k configure
```

#### 3b. Install zsh-syntax-highlighting

Run:
```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

Activate the plugin in `~/.zshrc`:
```
plugins=( [plugins...] zsh-syntax-highlighting)
```


#### 3c. Install zsh-autosuggesteions
```bash
git clone https://github.com/zsh-users/zsh-autosuggestions.git $ZSH_CUSTOM/plugins/zsh-autosuggestions
```

Activate the plugin in `~/.zshrc`:
```
plugins=( [plugins...] zsh-autosuggestions)
```


#### 3b. Install Fira Code font

A fantastic font for programming. Read more here [](https://github.com/tonsky/FiraCode)

Run the following command in your Terminal:
```bash
brew tap homebrew/cask-fonts && brew install --cask font-fira-code
```

Updates are installed by running:
```bash
brew update && brew upgrade font-fira-code
```


### 4. Install the GitHub CLI

The GitHub CLI makes a lot of features from the web interface conveniently available
from the command line.

```
brew install gh
```

Login with your GitHub credentials.

```
gh auth login
```


### Install pyenv

First make sure that Python build dependencies are in place.

Install Xcode Command Line Tools:

```bash
xcode-select --install
```

Then run:
```bash
brew install openssl readline sqlite3 xz zlib
```

To install Pyenv run:
```bash
brew install pyenv
```

And then configure Zsh for Pyenv run:
```bash
echo 'eval "$(pyenv init --path)"' >> ~/.zprofile

echo 'eval "$(pyenv init -)"' >> ~/.zshrc
```

### 6. Install Poetry

Poetry makes python packaging and dependency management easy and helps to ensure that
the packages we need for our projects play nicely with eath other.

It is important to install poetry in the following way to make it play nice with pyenv.

Run:
```bash
curl -sSL https://install.python-poetry.org | python3 -
```

```
poetry config virtualenvs.create false
```

This prevents Poetry from creating virtual environments. We are using conda for this.


### Install Docker
Run the following command in your command line:
```bash
brew install --cask docker
```

### Install Visual Studio Code

A fantastic IDE with great extensions, such as Jupyter notebook support.

Run the following command in your command line:
```bash
brew install visual-studio-code
```



### 4. Install pipx

pipx allows us to run python applications in an isolated environment independent of 
our other python environments.

```
brew install pipx
```

### 5. Install pre-commit

pre-commmit executes linters, format and other checkers conveniently everytime we
make a commit. This ensures that our code is always well formated and may even spot
simple issues in the code before they becomes a problem. If any issues are discovered
the commit will be aborted.

```
pipx install pre-commit
```





Voilà, everything should be ready!


## General process for setting up a project

### 1. Create a conda environment

It is a good idea to name the environment after your project. Depending on your
dependencies, you can also specifiy a different Python version

```
conda create -n <your-env-name> python=3.9
```

```
conda activate <your-env-name>
```


### 2. Move to the folder where you want to store your repositories

For example:

```
mkdir ~/github | cd ~/github
```


### 3. Setup the project with Poetry

```
poetry new <your-project-name>
```

pre-commmit executes linters, format and other checkers conveniently everytime we
make a commit. This ensures that our code is always well formated and may even spot
simple issues in the code before they becomes a problem. If any issues are discovered
the commit will be aborted.

```
poetry add pre-commmit --dev
```

Add .pre-commit-config.yaml and .flake8 from this repository to your project.
 
```bash
curl -LJO https://raw.githubusercontent.com/acnedata/project-setup-guide/master/.pre-commit-config.yaml
```

```bash
curl -LJO https://raw.githubusercontent.com/acnedata/project-setup-guide/master/.flake8
```

### 3. Initalize the folder as a git repository

Setting up the folder as a git repository.

```
git init
```

Making sure that pre-commit executes on commit.

```
pre-commit install
```

Voilà, now you are ready to commit your repository and start working on your project!


## Documentation

Homebrew: https://docs.brew.sh/FAQ

GitHub CLI: https://cli.github.com/manual/index

Conda environments: https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html

Poetry: https://python-poetry.org/docs/basic-usage/

pre-commit: https://pre-commit.com/