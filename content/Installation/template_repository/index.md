---
title: Preparing the template repository
weight: 2
---

## Start from GitHub template

Refer to [Research folder structure quick start guide ](/standard), clone the repository or download its content.

Make it a datalad repository with `datalad create -f -c text2git`


## Add submodules

You can either add submodules, or modify folders to become submodules.

Using datalad, you can create the submodules with:
```
datalad create -f -c text2git -d . 06_dissemination 
datalad create -d . 03_data/001_rawdata  
datalad create -d . 03_data/001_deriveddata
datalad create --no-annex -d . 04_data_analysis/001_analysiscode
datalad create -f -c text2git -d . 05_figures/990_shared_figures

```

Note that some of them use the text2git options, so that text will be added to git and not to git-annex.

You may have seen that the analysis code is a git-only repository, there will be no annexed file there. Alternatively, you may only use the text2git option with:
`datalad create -c text2git -d . 04_data_analysis/001_analysiscode`


(logic: 
create put datalad and git-annex info, `-c text2git` tells it to put text into git in that repo,
`-d .` tells that the supradataset or parent repository is located in the folder where the code is run,
`-f` will force the creation if the folder already exists.
`--no-annex` makes it a git-only repository)





## Add options for datalad

We will run `git annex config --set  annex.addunlocked true` in some datasets. There, annex files will not be locked when using datalad save or the scripts (takes twice as much space in non-windows computer, but will allow people to change binary files without needing to unlock them first).

```
git annex config --set  annex.addunlocked true
cd 06_dissemination 
git annex config --set  annex.addunlocked true
cd ../05_figures/990_shared_figures
git annex config --set  annex.addunlocked true
cd ../../
```

## Create repositories on GIN

You will need to add an application token for your user, then create the sibling with

`datalad create-sibling-gin tonictests/template_01 -s gin -r --api https://gindata.biologie.hu-berlin.de --existing reconfigure --credential juliencolomb`

- change the api with the address of your GIN instance, you do not have to specify the port.
- change credential with your username
- You can use a different organisation than G-Node, but since we created that one earlier, you may as well use it!
- you may change the name of the repository


The .gitmodules files needs to be corrected by hand at this point. The `URL` entry will not be correct. You need to modify it with `../template_01-06_dissemination` and so on. change every slash into `-`.

## Add scripts

You may want to add scripts for the udpates of repositories, see the [script section of this website](/tooling/synchronisationscripts/) and directly the github page at https://github.com/tonic-team/synchronisation_scripts

DO NOT USE the scripts to push the template, as scripts usually add other elements (extra submodules for example) you do not want here.

## Manual additions

You may want to add extra information and readme files, especially in the newly created submodules (the one with no `-f` above).



## Push data

you will first need to save changes `datalad save -r -m "template created"`
Then push your changes `datalad push --to gin -r`



## Clean history and rename branch

Until GIN is fixed, the sibling is 

and can recognize a "main" branch as the one to be used as head, the main bran

The following code will create a new branch "a_main" with all the template but no git commit history, so that research repositories start in a fresh state.

If a a_main branch already exist, you will need to erase it first:

- rename the branch and push with new name
- set the default branch to that new branch
- delete the a-main branch (using sourcetree)

We chose the name "a_main" so that GIN will use it as default in absence of master.
Depending on the tool you are using to clone the repository, 
you may have to checkout to that branch.

```
git checkout --orphan a_main
git add -A
git commit -m "Template initialisation"
git push --set-upstream origin a_main
```
Then make the a_main branch the default branch, on the browser (Settings::Branches).


