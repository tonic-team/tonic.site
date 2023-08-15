---
title: Home
# cSpell:ignore tonictool
# cSpell:ignore neuro
---

# GIN-Tonic: a digital shelf for your research files

{{% notice info %}}
This homepage works as a documentation for the tools created inside the Tonic project.
While the tools were developed in order to be integrated in the G-node Infrastructure GIN, they can be used independently.
{{% /notice %}}

## What is the Tonic project?

The Tonic project aims to develop a common file structure for (neuro-)scientific research projects,
as well as software to facilitate its use.
Our ultimate goal is to facilitate data, project and lab management
using an open source approach and technologically relatively simple approach.

[We are data managers](about) who support project templates and tooling for project structure creation, extension and validation.
This site documents the tools and gives guidelines on how to best use them.

## Overview

This project stands on a [research folder structure standard](standard),
which is a template of folders to give a similar organization of files for different research projects.
In contrast to the other tools, this first output can be used independently of a git-based technology.

The other tools are extensions making the work with git servers (GIN, GitHub or GitLab) easier.
Scripts synchronize content between machines and a Git server via a double click.
The [Tonic] application automates complex administrative tasks
like the creation of project repositories and user management.

## Development status

- Standard: version 2.4, Thorsten Arendt, Mittal, Deepti, Sehara, Keisuke, Cook, Tamara, & Julien Colomb. (2023). Folder structure template for research repositories (v2.4). Zenodo. https://doi.org/10.5281/zenodo.7763694
- Tonic: beta, stable version, no doi yet: https://github.com/G-Node/tonic
- Scripts: v.0.1.0, Colomb, Julien, & Koutsou, Achilleas. (2023). Tonic synchronisation scripts (0.1.0). Zenodo. https://doi.org/10.5281/zenodo.8249657

## Why was Tonic built

In the course of many research projects, digital data of various kinds is used and created.
This data is often organized in implicitly grown file structures,
so new collaborators or staff must understand the file structure before they can explore the content.
If research projects could adhere to a common file structure standard, data sharing and collaboration were more efficient.

All of them will be documented on this site.
Tonic has been initiated to augment the [GIN] (G-Node infrastructure), a version control system for neuroscientific data,
but isn't restricted to GIN.

[gin]: https://gin.g-node.org
[tonic]: /tooling/tonictool
