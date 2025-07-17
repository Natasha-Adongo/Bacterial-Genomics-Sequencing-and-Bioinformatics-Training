# Unix 2

![Conda](https://upload.wikimedia.org/wikipedia/commons/e/ea/Conda_logo.svg)

## What is Conda?

Conda is a package and environment manager that is by far the easiest way to handle installing most of the tools we want to use in bioinformatics.

## Why conda?

1. It's an open source management system
2. Conda quickly installs, runs and updates packages and their dependencies
3. Conda easily creates, saves, loads and switches between environments on your local computer
4. Conda as a package manager helps you find and install packages
5. If you need a package that requires a different version of Python, you do not need to switch to a different environment manager, because conda is also an environment manager

### What is an environment and why are they important in conda?

A conda environment is a directory that contains a specific collection of conda packages that you have installed.  For example, you may be working on a research project that requires NumPy 1.18 and its dependencies, while another environment associated with an finished project has NumPy 1.12 (perhaps because version 1.12 was the most current version of NumPy at the time the project finished)

Conda lets us easily create and manage separate environments to avoid these types of version conflicts, and automatically checks for us when we try to install something new (so we find out now, before we break something somewhere under the hood and have no idea what happened)

The benefits go further, like helping with reproducibility

### Getting and installing Conda

Conda comes in two broad forms: Anaconda and Miniconda. Anaconda is large with lots of programs in it already, Miniconda is more lightweight and then we can install just what we want.

To get started with Conda,

For linux users and Windows users on WSL

    curl -LO https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh

For MacOS users

    curl -LO https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-x86_64.sh

Now we can install that by running it as a bash command:
``` bash Miniconda3-latest-*.sh```

We need to interact with the following during installation:

    We will be asked to review the licence agreement. After pressing return/enter, we can view it and hit the space bar to advance. At the bottom, we need to type in yes to accept.
    It will then ask if the location is ok, hitting enter will place it in our current home directory, which is usually great.
    At the end it will ask if we want to initialize Miniconda3. There might be reasons to not want to do this, but until we hit one of those reasons, it probably makes things easier to say yes to that.

Great! Now we have conda installed. We just need to reload our current shell session, which we can usually do like so:

``` source ~/.bash_profile || source ~/.bashrc ```

And after that we should see a (base) at the start of our prompt, which tells us we are in the “base” conda environment. If the above didn’t work, you can also just open a new terminal window, and it should be updated there 👍

### Creating and navigating environments

#### Base environment

The “base” conda environment is, like it sounds, kind of our home base inside conda. We wouldn’t want to install lots of complicated programs here, as the more things added, the more likely something is going to end up having a conflict. But the base environment is somewhere we might want to install smaller programs that we tend to use a lot

#### Making a new environment

The simplest way we can create a new conda environment is like so:

``` conda create -n new_env ```

Where the base command is conda create, then we are specifying the name of our new environment with -n (here “new_env”). It will check some things out and tell us where it is going to put it, when we hit y and enter, it will be created.

#### Entering an environment

To enter that environment, we need to execute:

``` conda activate new_env ```

And now we can see our prompt has changed to have (new_env) at the front, telling us we are in that environment.

If we had forgotten the name, or wanted to see all of our environments, we can do so with:

``` conda env list ```

Which will print out all of the available conda environments, and have an asterisk next to the one we are currently in.

Other useful codes include:
```
conda list #shows you everything installed in your current environment
conda list -n [ENV NAME] #shows you everything installed in the specified environment

```

#### Exiting an environment

We can exit whatever conda environment we are currently in by running:

``` conda deactivate ```

### Setting up the appropriate channels for Bioinformatics

Once you have successfully created your new environment, one of the first key things is to add the Bioconda channel which houses alot of Bioinformatics tools

```
conda config --add channels defaults
conda config --add channels conda-forge
conda config --add channels bioconda
```

with the highest priority being the last entry

### Finding and installing packages

#### Searching for packages
The first thing I would suggest to do, whether I know if a program is conda-installable or not, is just search in a web-browser for “conda install” plus whatever program I am looking for.

#### Installing packages
``` conda create -n <environment_name> -c <channel_name> <package_name> ```

#### Uninstalling a package
If we wanted to remove a package, we would want to first be inside the environment that has the specific package:

```conda activate <env>```

And then we would run:

```conda uninstall <package>```

### Assignment
Install the following packages as conda environments assigning the package name as the environment name
1. spades
2. abricate
3. mlst
4. spatyper
5. sccmecfinder
6. fastqc
7. bbduk
8. mash
9. parsnp
10. iqtree2
