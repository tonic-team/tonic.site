---
title: Synchronisation scripts
---

## Our Goal

By double clicking one file, the local version and the server version of
the data will be synchronized.
Users can therefore use GIN-Tonic without using the command line,
and it automatize complex actions when there are submodules.

Here are listed our wish for the scripts
(the present version does not fulfill the whole list).

- works on windows, mac and linux
- works also when data is in (different) submodules
- works with GIN and other git based repositories

## Current Version

The current version of the file is:

- Some bash scripts (one master + other in `.script` folder)
- Uses GIN-cli commands
- Works for GIN repositories only,`
- Works with submodules (all synchronised using a single commit message).
- Also initialize submodules


We are testing different process and workflow to allow windows users to call the bash script, or use .bat scripts native to windows.

### Installation

One needs to install gin-cli, have a gin account and set server specific information. Refer to the help page of your instance of GIN for more information, or to https://github.com/tonic-team/synchronisation_scripts/tree/main/initialisation_scripts.

#### MAC/LINUX

- Copy the `sync` script and the `.script` folder found at
  [https://github.com/tonic-team/synchronisation_scripts](https://github.com/tonic-team/synchronisation_scripts) into you repository.
- open a terminal in that folder and type `chmod +x sync` so the file will be executed on a double click.
- double click the `sync` script.

#### Windows

- Copy the `sync`, the `sync.bat` and the `.script` files and folder found at
  [https://github.com/tonic-team/synchronisation_scripts](https://github.com/tonic-team/synchronisation_scripts) into your repository.
- [install bash for windows via cygwin](https://github.com/tonic-team/synchronisation_scripts/blob/main/windows-workflow.md)
- double click the `sync.bat` script.

## Sync Options

By setting one parameter at the start of the script at line 19, one can choose
how the script will deal with large files pushed via the git annex technology.
To set this up, open `sync` with a text editor and modify the option:

- `syncopt="download"`: Downloads and keeps all large file content on the local version.
- `syncopt="keep"`: Keeps existing local large file content, but do not downlaod extra files
- `syncopt="remove"`: Removing all local large file content once they are uploaded.

## The future

We are looking into using datalad instead of GIN-cli to allow more flexibility,
as well as the use of non-GIN repositories.
Creating a windows version of the script might then be easier.


## Troubleshooting

### Erasing a submodule

- use the webservice to delete the repo (optional)
- run `gin git rm -rf <path-to-submodule>` in a terminal in the main repo folder,  all submodule inside the path will be erase (-r is for recursive)
- run the sync script again
