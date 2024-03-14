# KAPy-local-example
Example of using KAPy in a local setting

# Creating your own local KAPy setup

The assumption here is that you want to setup a installation of KAPy, with the local scripts and configuration under version control in another Git repository. The following steps describe how this `KAPy-local-example` repository was created.

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

4. 
