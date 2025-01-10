# Tino Pai - a KAPy example repository

This repository provides a basic example of how the [KAPy workflow](https://github.com/Klimaatlas/KAPy/) can be used as part of a larger climate service project. 

The following documentation provides to approaches to using this repository. The first, 'Quick Start', makes a local copy of the repository that can be used to get up and running as quickly as possible. Alternatively, 'Custom Configuration' shows how to create a fully customised instance of a pipeline using KAPy.

# Quick Start

This configuration approach makes a direct copy of TinoPai into a local directory. 

1. Start by cloning the respository using http. 
```
git clone --recurse-submodules https://github.com/Klimaatlas/TinoPai.git
```

Some notes
* You won't be able to push changes back to the main TinoPai repository (as it is ready only), although you can still make changes and track them in the local repository. If you want to push to another remote repository, you will need to configure this manually.
* You may need to update the version of KAPy being using, as TinoPai is (by design) fixed to a specific version. The following will bring the local version up to date with the main branch of KAPy:
```
cd TinoPai/KAPy
git checkout main
git pull
```


# Custom Configuration

To start with, let us assume that we want to setup our own climate serivce processing chain, using [KAPy](https://github.com/Klimaatlas/KAPy/) as the main engine, with our configuration and local scripts place under version control in Git. For the sake of argument, we will refer to this project as `TinoPai`. The follow steps describe how the repository that you can see here was setup - by reproducing them on your own machine, you should be able to create your own local configuration.

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
git submodule add git@github.com:Klimaatlas/KAPy.git
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

7. That's basically the core of it - everything else is handled in the same way as normal KAPy. The rest of the work is populating the repository. This repository processes the data used in the KAPy tutorials and which needs to be downloaded and installed before use, in this case in the `./inputs` directory - see [KAPy Tutorial 1](https://github.com/Klimaatlas/KAPy/blob/main/docs/tutorials/Tutorial01.md) for information on where to obtain this data. The configuration files (e.g. the `./config` directory) are configured to run analysis, taking account of the new directory structure - see the `dirs` tag in `./config/config.yaml`. 

8. An important point to note is that the version of KAPy that is used in TinoPai is fixed, as part of the version control. If updates are made to the core KAPy workflow (e.g. on GitHub), these will not automatically propigate through to TinoPai, unless you explicitly ask for them. The way to do this is by first doing a pull in the KAPy directory. The change can then be made permanent by committing the changes e.g.
```
cd KAPy
git pull
cd ..
git add KAPy
git commit -m "Update KAPy to latest version"
```

9. That's it - you've got your own version of KAPy running locally, with everything you need under version control. *Tino pai*!


## More reading
* [Snakemake modules](https://snakemake.readthedocs.io/en/stable/snakefiles/modularization.html#modules)
* [Git submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules)

## Why Tino Pai?
Like KAPy, the name of this example repository is inspired by the *Te Reo Māori* language. Whereas *ka pai* (KAPy) can be translated as "good", *tino pai* is "very good" - reflecting the improvements that local customisations of KAPy should allow.
