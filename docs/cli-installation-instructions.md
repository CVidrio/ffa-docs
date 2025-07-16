# Installing the CLI

## Prerequisites

1. **Install Git**: [https://git-scm.com/downloads](https://git-scm.com/downloads). Verify that Git is installed by executing `git --version` in a shell.
2. **Install R** (Recommended version: v4.5.0): [https://www.r-project.org/](https://www.r-project.org/). Verify that R is installed by executing `R --version` in  a shell.  
3. **Install Pandoc** (the latest version): [https://pandoc.org/](https://pandoc.org/). Verify that Pandoc is installed by executing `pandoc --version` in a shell.

### Note for Windows Users

You may need to add Git, R and Pandoc to your `PATH` to run them from the command line.
The default paths for Git, R and Pandoc are:

```
C:\Program Files\Git\bin
C:\Program Files\R\R-4.5.0\bin
C:\Program Files\Pandoc
```
To update your `PATH`, edit your system environment variables from the settings menu.

## Instructions

First, install the [FFA Framework R package](https://github.com/rileywheadon/ffa-package).  
For details, see the [R package installation guide](r-installation-instructions.md).

### Step-by-Step Guide
1. Open a shell (terminal) and navigate to the directory where you want to install the framework.
2. Clone the GitHub FFA Framework repository by running the following command in a shell:

        git clone https://github.com/rileywheadon/ffa-framework.git

3. Navigate to the `ffa-framework` directory (e.g., `cd ffa-framework`). This directory contains a `renv.lock` file, which is used to manage R package dependencies.
4. Launch a command prompt with R. The `renv` package may install itself automatically. 
    If it does not, run `install.packages("renv")` to install it manually.
5. Load libraries from the `renv.lock` file by executing `renv::restore()`.
6. Install the FFA Framework R package using `devtools.install("path/to/ffa-package")`. You will need to replace `"path/to/ffa-package"` with the actual path to the package directory.
7. Exit the command prompt with `q()`.



---

This guide has been tested on Linux, Windows, and MacOS. 

Please submit a [Github Issue](https://github.com/rileywheadon/ffa-framework/issues) if you have any problems.

