---
title: 4 Data analysis
weight: 5
-----

{{% notice info%}} In a GIN workflow, it may also be a
submoduole, miror of a GitHub or GitLab repository. {{% /
notice %}}

## Content

This folder will contain either code (in python, R or
matlab), or textdescription of the analysis, or both.



## Organisation

The content may be organised following the different
experiments, or by different figures created or a mix of
these two. In addition we have 2 folder already present in
the template:

{{% expand "990\_code\_libraries" %}} Here comes the
dependencies of your software, it might be the dependencies
themselves, or a link/miror to the dependencies.

You may want to use a container technology to deal with your
code libraries. {{%/ expand%}}

{{% expand "991\_preregistration" %}} In order to prove that
your experimental design is preventing harking and
p-hacking, you should describe how you will analyze the data
before you actually start collecting it.

Any document that do that should be saved or mirrored here.
Note that you should have a time stamped version of this
file, proving it was produced before data acquisition. One
may use [osf](https://osf.io/) or
[zenodo](https://zenodo.org/) for this purpose. {{%/
expand%}}