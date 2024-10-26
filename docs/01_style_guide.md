# Style Guide for R Programming

This style guide provides guidelines for writing R code that is clean, readable, and maintainable. Adhering to these conventions will help ensure consistency across the codebase and make collaboration easier for team members.

## Table of Contents

1. [General Guidelines](#general-guidelines)
2. [Naming Conventions](#naming-conventions)
3. [File and Folder Naming](#file-and-folder-naming)
4. [Code Formatting](#code-formatting)
5. [Comments and Documentation](#comments-and-documentation)
6. [Function Design](#function-design)
7. [Package Management](#package-management)
8. [Session Management](#session-management)

## General Guidelines

- Aim for clarity and simplicity in your code.
- Write code that is self-explanatory. If a piece of code is complex, add comments to clarify.
- Keep functions and scripts focused on a single task.

## Naming Conventions

- Use **snake_case** for variable and function names (e.g., `calculate_mean`, `data_frame`).
- Constants should be written in **UPPER_SNAKE_CASE** (e.g., `MAX_VALUE`, `DATA_DIR`).
- Class names should use **PascalCase** (e.g., `MyClass`, `DataProcessor`).
- Avoid abbreviations unless they are widely understood.

## File and Folder Naming

- Prefix file and folder names with numbers to control their order in the project (e.g., `00_setup_guide.md`, `01_logging_guide.md`).
- Use **snake_case** for file and folder names, following the same convention as code (e.g., `data_management_guide.md`).
- Avoid spaces in file and folder names; use underscores `_` instead.

## Code Formatting
- Limit lines to 80 characters. You can make this easier by going to **Tools > Global Options > Code > Display** and ticking **Show Margin** in RStudio.
- Place spaces around operators (e.g., `x + y` instead of `x+y`).
- Use blank lines to separate logical sections of code.
- Place opening braces `{` on the same line as the statement.

### Example

```r
# Good formatting example
calculate_mean <- function(data_vector) {
  mean_value <- mean(data_vector)
  return(mean_value)
}
```

## Comments and Documentation
- Use comments to explain the "why" behind complex logic.
- Write documentation for all public functions, including:
    - A brief description of the function.
    - Input parameters and their types.
    - Return values and their types.
### Example of Function Documentation
```r
#' Calculate the mean of a numeric vector.
#'
#' @param data_vector A numeric vector.
#' @return The mean of the input vector.
#' @examples
#' calculate_mean(c(1, 2, 3))
calculate_mean <- function(data_vector) {
  mean(data_vector)
}
```

## Function Design
- Keep functions short and focused. Aim for a maximum of 20 lines of code.
- Use descriptive function names that clearly indicate the purpose of the function.
- Avoid side effects (e.g., modifying global variables).

## Package Management
- Use the **renv** package to manage project dependencies.
- After adding or updating a package, run **renv::snapshot()** to update the lock file.

## Session Management
- Avoid using **rm(list=ls())** in your code to clear the workspace. Instead, restart the R session using **Ctrl + Shift + F10** to ensure a clean environment.
- Ensure your scripts can run from start to finish without manual intervention. You can do this by using **Ctrl + Shift + S** to run all code from the beginning.

## Conclusion
Following these style guidelines will help ensure that your R code is consistent, readable, and maintainable. By adhering to these best practices, you contribute to a collaborative and efficient development environment.

