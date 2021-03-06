---
title: Quick start
weight: 1
# cSpell:ignore textreports
---

{{% notice info%}}
This is the minimal information you should read before using the standard.
It is organized via when you will use what folder and does not go into details.
{{% / notice %}}

{{% notice warning%}}
You may **delete folders** you are not using, but please do not rename the existing ones,
as it would probably break the tools made available and reduce the portability of your data.

If you want to **add new folders**, please tell us so we can include them in a future version of the template
(so others needing similar structures would name them identically).
{{% / notice %}}

### Prior to data acquisition

- save all documents related to research planning in the **01-Project_management** folder,
  and update material and methods information as soon as possible.
  For instance, indicate all information about reagents at the time or purchase.
  And put any code or variable files created for data acquisition in the 02_material_methods folder.

### Data acquisition and analysis

- Data is organized first following experiments, as subfolder of the **\*03_data** folder.
  Make sure to describe every experiment in a readme file and link to the adequate files saved in 02_material_methods.

- Refer to a data organization guide or a data management plan to organize the files in that folder.
  Any file coming directly from your hardware (raw data) or that is manually created (raw, derived data, or manually analysed data)
  should be in the experiment folder.

- Any file created automatically during the analysis and that is easy to recreate should be saved in **03_data/990_processed_data**:
  it will not be included in the long term storage or publication of the data.

- The **04_data_analysis** folder should only include code and documentation of the analysis.
  If you are using excel to analyse the data, put the files in the processed_data
  and only add some text describing the analysis in the analysis folder.
  If you are using notebooks in python or R for analysis, their place is here.

- The output of your analysis (figures, and pdf reports outputs of notebooks)
  should be saved in the **05_figures** or the **06_disseminations/01_report_conferences/01_textreports** folders, respectively,
  in order to facilitates sharing with non-coders.

### Manuscript preparation

- Put figures ready for publication in the **05_figures/shared_figures** folder.

- Put the manuscript (or some important versions of it, if using an external tool for writing it)
  in the **06_disseminations/02_manuscripts** folder.
  You may want to use full URL to embed figures in the manuscript if the repository is open.

{{% notice note%}}
Having figures saved independently of manuscripts will allow you to reuse the same figures
for different dissemination outputs (poster, presentation, manuscripts).

When using a reference managers, you may want to describe its use in a readme file
and save a `.bib` export of the bibliography in the manuscript folder.
{{% / notice %}}
