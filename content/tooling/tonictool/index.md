---
title: Tonic forms
---

Tonic will be a tool to facilitate the administration of GIN repositories.

## Create a repository

By login with its GIN account, the user is able to create a repository insite an organisation where he does not have admin rights.
The repository is filled with a template.
The template can be the [research folder structure standard](/standard/),
or a derived template using submodules.

### Installation

- Tonic can be installed via docker.
- A specific user (with admin rights) shoud be added to the owner
  team of the organisation.
- A template should be added to the GIN server (one can for example mirror the [research folder structure standard](/standard/).
- Optionally [synchronization scripts](/tooling/synchronisationscripts/) may be added to the template.
- A json file provide information about the GIN server,
  the specific user credentials and the template to be used.
- The user can then access the form via a URL.
