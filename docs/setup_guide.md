# Setup Guide for Statistical Analysis Projects

Welcome to the setup guide! This document outlines the steps to set up your statistical analysis project using R, `renv`, and the `targets` package. Following these guidelines will help ensure a consistent and reproducible environment for all team members.

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Creating a New Project](#creating-a-new-project)
3. [Setting Up renv](#Setting-up-renv)
4. [Setting Up targets](#setting-up-targets)
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
This command will create a new library for your project and a lock file (renv.lock) that records package versions.

3. To install packages and add them to your renv.lock file, use:
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
The targets package streamlines workflows for reproducible research, helping to organize and automate the data analysis process.

To set up targets, follow these steps:

1. Install the package, if you haven't done so:
```r
install.packages("targets")
```

2. Create a file named _targets.R in the root of your project directory. This file will define your analysis workflow.

3. Inside the _targets.R file, load the necessary libraries and set options. Here’s a simple template to get you started:
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

## Example project folder
To see a recommended folder structure for your project, refer to the templates/example_project/ folder in this repository. This structure includes folders for data, R scripts, output, and more, providing a clear organization for your project files.