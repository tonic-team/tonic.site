---
title: Synchronisation scripts
---

## Our Goal

By double clicking one file, the local version and the server version of
the data will be synchronized.
The script ask for a commit message that will be used for all repositories update, and then update the repositories with the server version.

Users can therefore use GIN-Tonic without using the command line,
and it automatize complex actions when there are submodules.

You will find the scripts at https://github.com/tonic-team/synchronisation_scripts.

## version 0.0.9

In this version, we have two possibilities. One can either use an older version based on GIN-cli and running via a bash script, or use the datalad-based script. Windows user should opt for the latter one.
If you want both, you will need to combine the `.script` folders.

The datalad scripts contains one bash and one .bat script to be executed on UNIX or windows computer, both should work out of the box, as they are only calling a python script.
The GIN-cli based script will also initializes the lab_report repository.

## Installation

Executable scripts should be in the main parent folder of the parent repository, the .scripts hidden folder should also be copied there. If you want to have both scripts available, you will need to combine the two .scripts folder. This is best done in a template repository.

### Make it executable

While .bat scripts are executable per default on windows machine, you will need to make the UNIX script executable. For this you will need to run `chmod +x sync_unix` or `chmod +x sync_gin_unix` in the parent repository folder, depending on which script you want to use.

### Git annex - file locking

The GIN-cli script will keep files unlocked per default (as [GIN-cli does](https://gin.g-node.org/G-Node/Info/wiki/GIN+CLI+Usage+Tutorial#file-locking).

To get the same behavior using the datalad script, one needs to run `git annex config --set  annex.addunlocked true` in the repository (this will modify the `annex branch` of your repository.)

### Requirement

### GIN-cli scripts

One needs to install gin-cli, have a gin account and set server specific information. Refer to the help page of your instance of GIN for more information, or to https://github.com/tonic-team/synchronisation_scripts/tree/main/initialisation_scripts.

### datalad scripts

The datalad scripts require datalad to be installed, and a ssh connection between your computer and the online repository.
It also needs python 3 to be installed (this is usually also a requirement for datalad).

_The \`set a ssh connection\` step may be a bit complicated, please refer also to the [datalad handbook](http://handbook.datalad.org/en/latest/index.html#)._ My advice is to use [Rstudio to set your ssh key](https://happygitwithr.com/ssh-keys.html), it is much faster than going through the command line interface.

## Dropping files

Large files can be erased from the hard disc (this is done only if the server version has been uploaded successfully). The two scripts use different strategies to set this up.

### GIN-cli script

By setting one parameter at the start of the script at line 19, one can choose
how the script will deal with large files pushed via the git annex technology.
To set this up, open `sync` with a text editor and modify the option:

- `syncopt="download"`: Downloads and keeps all large file content on the local version.
- `syncopt="keep"`: Keeps existing local large file content, but do not downlaod extra files
- `syncopt="remove"`: Removing all local large file content once they are uploaded.

### Datalad script

At the end of the process, the terminal will ask you whether you want to drop the last uploaded files, and then if you want to drop all files.

To download all files, you will need to use the terminal with the `datalad get . -r` function (this one will download all files, including in all submodules).

## History

This work was started at <https://gin.g-node.org/gin4RRI/gin-scripts/>, and then moved to GitHub (in order to get all work under the same team umbrella.) We first work on scripts using GIN-CLI, as the tonic template did not have submodules.
We then moved to use datalad in scripts, as it is easier to make it work on windows machine, and make it probably easier to handle on the long run, as datalad is made to work with submodules (GIN-Cli is not).

## Troubleshoot

### OSX

- one needs to install datalad via homebrew **and** via pip3

### Windows

- It may be tricky to install everything on Windows. Especially ssh keys do not work the same. Reinstall everything fresh when you encounter an issue with the installation.

### Data on server

- If you are using a linux server to store your data, you will not be able to run the .bat script. We do not have yet a solution for this use case.

### Erasing a submodule

- use the webservice to delete the repo (optional)
- run `gin git rm -rf <path-to-submodule>` in a terminal in the main repo folder, all submodule inside the path will be erase (-r is for recursive)
- run the sync script again
