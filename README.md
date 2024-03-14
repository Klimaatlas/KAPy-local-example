# Tino Pai - a KAPy example repository

This repository provides a basic example of how the [KAPy workflow](https://github.com/Klimaatlas/KAPy/) can be used as part of a larger cliamte service project. 

To start with, let us assume that we have want to setup our own climate serivce processing chain, using [KAPy](https://github.com/Klimaatlas/KAPy/) as the main engine, with our configuration and local scripts place under version control in Git. For the sake of argument, we will refer to this project as `TinoPai`. The follow steps describe how the repository that you can see here was setup - by reproducing them on your own machine, you should be able to create your own local configuration.

1. First, create your own repository where you wish to store your data. This can be in GitHub, GitLab, or locally git. If you want to follow along in this example, it's easiest just to create a test setup on your local machine like so:

```
mkdir TinoPai
cd TinoPai
git init
```
2. You may want to create some directories to store your configurations, inputs and outputs.
```
mkdir config
mkdir inputs
mkdir outputs
```
3. Now comes the key trick for integrating the pipeline - we add the KAPy repository as a git submodule, like so:
```
git submodule add https://github.com/Klimaatlas/KAPy.git
```
You can read lots more about exactly how Submodules work in Git here: https://git-scm.com/book/en/v2/Git-Tools-Submodules We're not going to go into the details, other than to note that they do work very nicely for this application.

4. Commit the change
```
git commit -m 'Add KAPy submodule'
```
5. Now explore the `./KAPy` directory. You will see all of the content as you know it directly from KAPy, but now integrated directly into your own repository.

6. Unfortunately snakemake isn't able to work with this setup directly, so we need to tell it how to incorporate KAPy into TinoPai. We do this via a Snakefile, where KAPy is explicitly imported into the local workflow. Copy the following text into a file and save it as `Snakefile` in the root directory of the `TinoPai` repository (or alternatively, download it from here

```Snakemake
module KAPy:
    snakefile:
        "KAPy/workflow/Snakefile"

use rule * from KAPy 
```

7. 


## More reading
* [Snakemake modules](https://snakemake.readthedocs.io/en/stable/snakefiles/modularization.html#modules)
* [Git submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules)

## Why Tino Pai?
Like KAPy, the name of this example repository is inspired by the *Te Reo Māori* language. Whereas *ka pai* (KAPy) can be translated as "good", *tino pai* is "very good" - reflecting the improvements that local customisations of KAPy should allow.
