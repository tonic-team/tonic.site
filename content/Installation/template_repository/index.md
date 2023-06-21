---
title: Preparing the template repository
weight: 2
---

> Requirement: datalad installed, some element will only run on bash, ssh and token access for datalad to talk to the GIN instance, and the corresponding user should have owner rights to the G-Node organisation.

## Start from GitHub template and add submodules

Refer to [Research folder structure quick start guide ](/standard), clone the repository or download its content.

Make it a git repository and add submodules, or modify folders to become submodules.

Using datalad, you can do all that with:

```
datalad create -f -c text2git

datalad create -f -c text2git -d . 06_dissemination
datalad create -d . 03_data/001_rawdata
datalad create -d . 03_data/001_deriveddata
datalad create  -c text2git -d . 04_data_analysis/001_analysiscode
datalad create -f -c text2git -d . 05_figures/990_shared_figures

```

Note that some of them use the text2git options, so that text will be added to git and not to git-annex.
 
> Because the tonic application does not support repositories without annex, we did not use the --no-annex option for the code repository, this might be done in the repositories later on. (https://github.com/G-Node/tonic/issues/52) 

You may have seen that the analysis code is a git-only repository, there will be no annexed file there. Alternatively, you may only use the text2git option with:
`datalad create -c text2git -d . 04_data_analysis/001_analysiscode`

(logic:
create put datalad and git-annex info, `-c text2git` tells it to put text into git in that repo,
`-d .` tells that the supradataset or parent repository is located in the folder where the code is run,
`-f` will force the creation if the folder already exists.
)

## Add options for datalad and add readme files

We will run `git annex config --set  annex.addunlocked true` in some datasets. There, annex files will not be locked when using datalad save or the scripts (takes twice as much space in non-windows computer, but will allow people to change binary files without needing to unlock them first). We will also populate readme file and make sure they are not git-annexed by setting md files to be added on git on the repository not having the "text2git" option.

```
git annex config --set  annex.addunlocked true
cd 06_dissemination
git annex config --set  annex.addunlocked true
cd ../05_figures/990_shared_figures
git annex config --set  annex.addunlocked true
cd ../../

echo "**/*.md annex.largefiles=nothing" >> 03_data/001_rawdata/.gitattributes
echo "**/*.md annex.largefiles=nothing" >> 03_data/001_deriveddata/.gitattributes

echo "
Here comes the raw data (that is data coming directly from the research hardware used, or manually entered (for example in spreadsheets))

It is good practive to never modify files here, make copies in the derived data folder if you need to clean the data." >> 03_data/001_rawdata/README_dataraw.md

echo "
Here comes derived data, usually this repository would be:

- trashed if the raw data is published
- published if the raw data is archived
" >> 03_data/001_deriveddata/README_dataderived.md

echo "
# Figures

Put here figures/graphs you want to share or use in dissemination files (poster/presentation)

" >> 05_figures/990_shared_figures/README_figures.md

echo "
# code for analysis repository

Note: This is a not pure git repository.
If you want a pure git repository, create a new one manually and use only datalad scripts.

" >> 04_data_analysis/001_analysiscode/README_analysis-code.md

```

## Create repositories on GIN

You will need to add an application token for your user, then create the sibling with

```
datalad create-sibling-gin G-Node/template_03 -s gin -r --api https://gindata.biologie.hu-berlin.de --existing reconfigure --credential juliencolomb
```

- change the api with the address of your GIN instance, you do not have to specify the port.
- change credential with your username
- You can use a different organisation than G-Node, but since we created that one earlier, you may as well use it!
- you may change the name of the repository

PS: you need to have an application token for datalad to do this.

## Correct .gitmodules

The .gitmodules files needs to be corrected by hand at this point. The `URL` entry will not be correct. You need to modify it with `../template_03-06_dissemination` and so on. change every slash into `-`.

```
open .gitmodules
```

## Add scripts

You may want to add scripts for the udpates of repositories, see the [script section of this website](/tooling/synchronisationscripts/) and directly the github page at https://github.com/tonic-team/synchronisation_scripts

DO NOT USE the scripts to push the template, as scripts usually add other elements (extra submodules for example) you do not want here.

## Manual additions

You may want to add extra information and readme files, especially in the newly created submodules (the one with no `-f` above).

Putative changes:

- modify readme files
- add a `.Rprofile` file to give info to Rstudio users
- 


## Push data

you will first need to save changes `datalad save -r -m "template created"`
Then push your changes `datalad push --to gin -r`

## Clean history and rename branch

Since you may have made several save at this point, we want to clean the history, so that new repositories created with the template start with 1 or 2 commits.

To do so, we will create a new branch and rename the master branch "oberste", and delete the master branch on gin:

Let's first rename the master branch:
```
git branch -M oberste
git push --set-upstream gin oberste
git push -d gin master

```

Now, let's create a new branch with empty history

```
git checkout --orphan a_main
git add -A
git commit -m "Template initialisation"
git push --set-upstream gin a_main
```

Then **make the a_main branch the default branch**, on the browser (Settings::Branches).

Note: If a a_main branch already exist, you will need to erase it first:

`git branch -d a_main``
`git push -d gin a_main``


> The clean branch is called a_main because in absence of "master"" branch, GIN takes alphabetical order for the default branch.

> Depending on the tool you are using to clone the  repositories created from the template,
you may have to checkout to to the a_main branch to see the content.





