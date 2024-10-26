# Project Structure Guide

Organizing your project into a clear folder structure ensures a reproducible, logical, and easy-to-navigate workflow. Below is a suggested structure for statistical analysis projects.

## Root Folder Structure

```plaintext
project-name/
├── code/
│   ├── analyses/
│   └── functions/
├── data/
│   ├── raw/
│   └── processed/
├── outputs/
├── renv/
├── .Rprofile
├── _targets.R
└── .gitignore
```
**Folder Descriptions**

1. code/
- Houses all project code, organized into two main subfolders:
    - **analyses/** — Scripts organized by analysis task (e.g., **data_preparation.R**, **model_fitting.R**, **visualization.R**). Include a main script (e.g., **main_analysis.R**) that runs the full pipeline.
    - **functions/** — Custom R functions used across analyses. Keep code modular and reusable by saving functions in separate files according to purpose (e.g., **functions/data_cleaning_functions.R**).
- Tip: Prefix analysis scripts with a number if they should be run in a specific order, such as **01_data_preparation.R**.

2. data/
- Contains all raw and processed data files, with two main subfolders:
    - raw/ — Stores original data files, kept unchanged to ensure reproducibility.
    - processed/ — Contains data files that have been transformed or cleaned for analysis.
**Note**: Avoid storing sensitive or large data files directly in version control.

3. outputs/
- Used for results generated from the analysis, such as tables, plots, and model summaries.
- Consider organizing subfolders by type of output (e.g., **outputs/tables/**, **outputs/plots/**).
- Ideal for storing intermediate results and any exported reports.

4. **renv/** and **.Rprofile**
- **renv** manages package versions to ensure that analyses can be run reproducibly with the same dependencies.
- The **.Rprofile** file initializes renv automatically when the project is opened, ensuring that the correct environment is loaded.

5. _targets.R
- The configuration file for the **targets** package, which manages the pipeline workflow.
- Defines each step of the analysis pipeline as a target, specifying dependencies and making it easy to rerun only the necessary steps when data or code changes.

.gitignore
- Specifies which files or folders Git should ignore. This may include:
    - Large or sensitive data files
    - **.Rhistory** and **.RData**
    - Outputs that can be regenerated, like plots or tables
- Helps keep the repository focused and clean.

## Recommended File Naming Conventions

    Use descriptive names with lowercase letters and underscores (_) to separate words, avoiding spaces.
    Add 00_, 01_ prefixes for ordered files, and consider adding README.md files in key folders for quick reference.

## Additional Tips

    Version Control: Ensure all scripts, documentation, and non-sensitive results are version controlled using Git.
    Readme File: Include a README.md file in the project root folder with a project overview, usage instructions, and key contacts.