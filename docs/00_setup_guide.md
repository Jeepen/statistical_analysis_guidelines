# Setup Guide for Statistical Analysis Projects

Welcome to the setup guide! This document outlines the steps to set up your statistical analysis project using R, `renv`, and the `targets` package. Following these guidelines will help ensure a consistent and reproducible environment for all team members.

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Creating a New Project](#creating-a-new-project)
3. [Setting Up renv](#Setting-up-renv)
4. [Setting Up targets](#setting-up-targets)
5. [Log Files](#log-files)
5. [Example Project Structure](#example-project-structure)

## Prerequisites

Before starting, ensure you have the following installed:

- R
- RStudio (recommended for an integrated development environment)

## Creating a New Project

1. Open RStudio.
2. Go to **File > New Project**.
3. Select **New Directory** and then **New Project**.
4. Name your project (e.g., `my_analysis_project`).
5. Choose a directory where the project will be created.

## Setting Up renv

`renv` is a powerful package that manages project-specific R package libraries, ensuring that your project uses consistent package versions for reproducibility. 

To set up `renv`, follow these steps:

1. Install the package if you haven't already. Open the R console within your new project and run:

```r
install.packages("renv")
```

2. Initialize renv by executing:
```r
renv::init()
```
This command will create a new library for your project and a lock file (**renv.lock**) that records package versions.

3. To install packages and add them to your **renv.lock** file, use:
```r
renv::install("package_name")  # Replace "package_name" with the actual package name
```

4. After making changes to your package environment (e.g., adding or removing packages), update the renv.lock file by running:
```r
renv::install("package_name")  # Replace "package_name" with the actual package name
```r
renv::snapshot()
```

5. After defining your project dependencies, you can restore the required packages at any time by running:
```r
renv::restore()
```

## Setting Up targets
The targets package streamlines workflows for reproducible research, helping to organize and automate the data analysis process.

To set up targets, follow these steps:

1. Install the package, if you haven't done so:
```r
install.packages("targets")
```

2. Create a file named **_targets.R** in the root of your project directory. This file will define your analysis workflow.

3. Inside the **_targets.R file**, load the necessary libraries and set options. Here’s a simple template to get you started:
```r
library(targets)
library(magrittr)

tar_option_set(packages = c("dplyr", "ggplot2"))  # Specify any packages your analysis will use

list(
  tar_target(raw_data, read.csv("data/mtcars.csv")),   # Load data
  tar_target(summary_stats, summary(raw_data)),        # Compute summary statistics
  tar_target(plots, {
    ggplot(raw_data, aes(x = wt, y = mpg)) +
    geom_point() +
    labs(title = "MPG vs Weight")
  })
)

```

4. In this example, the workflow is set up to load the mtcars dataset, compute summary statistics, and create a scatter plot of MPG against weight.

## Log Files

Log files play a crucial role in documenting the analysis process. They can include information about script execution, parameters used, and any errors encountered during analysis. Proper logging enhances reproducibility and facilitates debugging.

### Best Practices for Logging

- **Create a logs/ Directory**: Store all log files in the `logs/` folder to keep them organized and easily accessible.
- **Use Clear Naming Conventions**: Name your log files descriptively (e.g., `data_cleaning_log.txt`, `eda_log.txt`) to indicate their contents and purpose.
- **Record Important Events**: Log key events, such as when scripts are run, significant changes in analysis methods, or results of specific analyses.
- **Include Timestamps**: Include timestamps in your log entries to track when specific actions occurred.

For more detailed guidance on logging practices, refer to the [Logging Guide](docs/logging_guide.md).

## Example project structure
To see a recommended folder structure for your project, refer to the `templates/example_project/` folder in this repository. This structure includes the following components, which will help maintain organization and clarity in your project:

- **data/**: This folder is designated for all raw and processed data files. Keep your original data files here to ensure they are preserved. You can also store any cleaned or transformed datasets for easy access during analysis.

- **R/**: Place your R scripts in this folder. Each script should correspond to specific tasks or analyses you are performing. For example, you might have scripts for data cleaning (`clean_data.R`), exploratory data analysis (`eda.R`), and final reporting (`report.R`).

- **outputs/**: This directory is intended for saving generated outputs, such as figures, tables, and reports. Organizing outputs separately helps keep your project tidy and allows for easier referencing during analysis.

- **logs/**: This folder is where you can store log files generated during your analysis. Logs can include information about the execution of scripts, any errors encountered, and the parameters used in your analysis. Keeping logs is crucial for reproducibility and helps in debugging any issues that arise.

- **.Rproj**: This is the RStudio project file. It encapsulates your project's settings and helps manage files and directories within RStudio.

- **renv.lock**: This lock file is automatically generated by `renv` and captures the exact versions of the R packages used in your project. This ensures reproducibility, allowing anyone who accesses your project to replicate the environment.

- **_targets.R**: This is the main file for the `targets` package. It defines your analysis pipeline, detailing the steps from loading data to generating outputs.

By following this structured approach, you can enhance the reproducibility and clarity of your statistical analysis projects, making it easier for you and your team to navigate the work and collaborate effectively.

---
