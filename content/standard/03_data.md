---
title: 3 Data folder
weight: 4
---

{{% notice info%}}
This may contain experiment sub-folders that would be shared with different people. The use of submodule technology may help with that.
{{% / notice %}}

## Content

This folder will contain datasets, that is information collected, gathered or created during the reseach project. One project usually has several experiments and each experiment shall get its own folder.

## Organisation

The organisation is quite loose for the time being, but specific templates for your data types may exist (see BIDS format for neuroimaging data for example).

- Each experiment/dataset gets one subfolder. Here comes data that should be saved for long term storage, published and/or should be shared with collaborators. Experiment subfolder start with a 3 digits number.

- Derivative data that can be easily recreated (and that should therefore not be stored for the long term) should go in a different folder **990_processed data**. You may want to split the data between experiments there too.
