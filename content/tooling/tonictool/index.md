---
title: Tonic forms
---

Tonic is a tool to facilitate the administration of GIN repositories.

## Create a repository

By login with its GIN account, the user is able to create a repository inside an organisation where he does not have admin rights.
The repository is filled with a template.
The template can be the [research folder structure standard](/standard/),
or a derived template using submodules.

### Installation

1. On the GIN instance:

- Create an organisation for the laboratory.
- A specific user (with admin rights) shoud be added to the owner
  team of the organisation.
- A template should be added to the GIN server (one can for example mirror the [research folder structure standard](/standard/).
- Optionally [synchronization scripts](/tooling/synchronisationscripts/) may be added to the template.
- Create a json file provide information about the GIN server,
  the specific user credentials and the template to be used.

2. Tonic installation

- Get tonic from Github
- Get you json file ready and create a `.db` file to save tonic log.
- Follow instructions (in the docs) to install it via docker.
