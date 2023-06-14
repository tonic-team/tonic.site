---
title: Preparing the template repository
weight: 2
---

## Start from GitHub template

Refer to [Research folder structure quick start guide ](/standard), clone the repository or download its content

## Add submodules

You can either add submodules, or modify folders to become submodules.

## Add options for datalad

You should create datalad repositories with `datalad create -force -c text2git -r``

Note that you may not want to use the text2git option for all submodules, you can modify the .gitattribute file by hand to modify the options.

If you want to have files unlocked by default, run `git annex config --set  annex.addunlocked true`.

## Clean history

In order for research repositories to start with

The following code will create a new branch "a_main" with all the template but no git commit history, so that research repositories start in a fresh state.

If a a_main branch already exist, you will need to erase it first:

- rename the branch and push with new name
- set the default branch to that new branch
- delete the a-main branch (using sourcetree)

We chose the name "a_main" so that the

````
git checkout --orphan a_main
git add -A
git commit -am "Template initialisation"
git push --set-upstream origin a_main
```
Then make the a_main branch the default branch, on the browser (Settings::Branches).


````
