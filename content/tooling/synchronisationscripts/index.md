---
title: Synchronisation scripts
---

## Our Goal

By double clicking one file, the local version and the server version of
the data will be synchronized.
Users can therefore use GIN-Tonic without using the command line,
and it automate complex action when there are submodules.

Here are listed our wish for the scripts, note that the present version does not fulfil the whole list.

- work on windows, mac and linux
- work also when data is in (different) submodules
- work with GIN and other git based repositories

## Current Version

The current version of the file is:

- Some bash scripts (one master + other in `.script` folder) 
- Work for GIN repositories only,`
- Work with submodules (all synchronised using a single commit message).
- Also initialise submodules (needs SSH access)


Note that synchronisation does work with a gin identification, but the initialisation of the script requires SSH access (gin does not support submodules).

We are testing different process and workflow to allow windows users to call the bash script.

### Installation

#### MAC/LINUX:

- Copy the `sync` script found at https://github.com/tonic-team/synchronisation_scripts into you repository.
- open a terminal in that folder and type `chmod +x sync` so the file will be executed on a double click
- double click the `sync` script.

#### Windows

- Copy the `sync` and the `sync.bat`scripts found at https://github.com/tonic-team/synchronisation_scripts into you repository.
- [install bash for windows via cygwin](https://github.com/tonic-team/synchronisation_scripts/blob/main/windows-workflow.md)
- double click the `sync.bat` script.

### Options

By setting one parameter at the start of the script at line 19, one can choose
how the script will deal with large files pushed via the git annex technology. To set this up, open `sync` with a text editor and modify the option:

- `syncopt="download"`: Downloads and keeps all large file content on the local version.
- `syncopt="keep"`: Keeps existing local large file content, but do not downlaod extra files
- `syncopt="remove"`: Removing all local large file content once they are uploaded.

## troubleshooting

### erasing a submodule

- use the webservice to delete the repo (optional)
- run `git rm <path-to-submodule` in a terminal in the main repo folder
- run the sync script again