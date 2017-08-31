Introduction to R | Getting started
================
EcoHealth Alliance

<img src = "rlogo.png" style="position:absolute;top:0px;left:0px;"/>

Content
-------

[What is R?](#whatr)

[Why R?](#whyr)

[Getting started: Installing R](#rinst)

[Getting started: Installing RStudio](#rsinst)

[RStudio Interface](#interf)

[Basic Operations](#oper)

[Working directory](#wdir)

[Libraries & Packages](#lib)

[Getting Help](#help)

<a name = "whatr"><a/>What is R?
--------------------------------

R is a software environment and language that enables:

-   data manipulation
-   calculation
-   graphical display

------------------------------------------------------------------------

<a name = "whyr"><a/>Why R?
---------------------------

-   It is free and open software, which means that it is flexible enough to create packages for specific computational purposes

-   R functions and packages are extremely well documented and information is readily available online.

-   Uses a fairly high level language (compared to C++ for example)

------------------------------------------------------------------------

<a name = "rinst"><a/>Getting started | Installing R
----------------------------------------------------

1.  Go to <https://www.r-project.org/>
2.  Click on **CRAN** on the left bar under **Download**

<div calss = "midcenter">
<img src = "rinstall.png"<img>
<div>

1.  Choose a download website from the list
2.  Choose your operating system (Windows, MAC, Linux)
3.  Click **base**
4.  Click on **Download R.3.2.3 for** your operating system (OS)
5.  Choose default answers for all questions

R is installed! You should now have an R icon on your desktop.

### Exercise 1

Install R on your computer. Make sure that you choose the correct operating system.

------------------------------------------------------------------------

<a name = "rsinst"><a/>Getting started | Installing RStudio
-----------------------------------------------------------

1.  Go to <https://www.rstudio.com/>
2.  Click con **Download RStudio**
3.  Click con **Download RStudio Desktop**
4.  Look for the **Open Source Edition column**
5.  Click on the **Download RStudio Desktop** button
6.  Then choose your OS under **Installers for Supported Platforms**
7.  Download the .exe file and run it choosing default answers for all questions

### Exercise 2

Install RStudio on your computer.

------------------------------------------------------------------------

<a name = "interf"><a/>RStudio Interface
----------------------------------------

When you open RStudio you will notice that there are several windows:

1.  Script window
2.  Console window
3.  Workspace/history window
4.  Files/plots/packages/help window

<div calss = "midcenter">
<img src = "rstudio.png"<img>
<div>


Let's open a new script:

1.  Go to the menu and click con **File**
2.  Scroll to \*\*New File\*
3.  Choose \*\*R Script\*

A new *script* window should open. You can also do this by simply typing **CTRL + Shift + N**

<a name = "oper"><a/>Basic Operations
-------------------------------------

R can be used as a calculator to perform basic mathematical operations.

For example:

``` r
2 + 2
```

    ## [1] 4

To do so you must type the operation in your script window and then press **CTRL + ENTER**. Make sure the crusor is on the command line.

You can also type the operation in the **Console** window and press **Enter**

These are some mathematical operations R is capable of doing:

|  Operator |    Description    |
|:---------:|:-----------------:|
|     +     |      Addition     |
|     -     |    Subtraction    |
|     \*    |   Multiplication  |
|     /     |      Division     |
| ^ or \*\* |   Exponentiation  |
|    sqrt   |    Square root    |
|    log    | Natural logarithm |
|   log10   |  Base 10 logaritm |

Notice that the presence of parentheses *()* indicates which operations should be carried out first.

``` r
2 + 2 * 10
```

    ## [1] 22

is different from

``` r
(2 + 2) * 10
```

    ## [1] 40

### Exercise 3

Use R to carry out the following calculations

<div class="columns-2">

1.  3 + 10 + 2
2.  20 \* 4
3.  sqrt(16) - 10
4.  (15/3) \* (10^2)
5.  (2 + 8) \* log10(100) / 5

<div>

------------------------------------------------------------------------

<a name = "wdir"><a/>The Working Directory
------------------------------------------

The working directory is the folder in which you are currently working in. This means that R will:

-   Look in this folder first for any file you load
-   Write all outputs in this folder

To know what is your current directory you only need to type:

``` r
getwd()
```

You are able to change your working directory through the RStudio Interface by:

1.  Going to the **Session** menu
2.  Scroll to **Set Working Directory**
3.  **Choose Directory**

A file browser window should open and you may choose the appropriate folder.

You can also check what is currently within the directory by using

``` r
dir()
```

Another way to change the working directory is through the `setwd()` function.

``` r
setwd("C:/Path/MyNewDir")
```

### Exercise 4

1.  Create a folder called *R\_wkshp* under **Documents**
2.  Find your current working directory
3.  Set your working directory to the *R\_wkshp* folder you just created
4.  Check if your current directory is different now

------------------------------------------------------------------------

<a name = "lib"><a/>Libraries & Packages
----------------------------------------

R can also carry out a variety of statistical analyses that are available in *packages* or *libraries*. Some of these are downloaded upon R installation, however some of the more specific computations require that you download additional *packages*.

**View installed packages:** You can view installed packages by clicking on the **Packages** tab in the bottom-right window. Alternatively, you may use the command line and type:

``` r
library("package.name")
```

And a list of packages should appear in the *console* window.

**Installing Packages:** If we wish to install a package, we can click on the **Install** button on the \*\*Package\* tab and type in the name(s) or the package(s) we need.

You can also do this through the command line by using the install.packages() comand. It is important that the name of the package be enclosed in apostrophes.

**Loading Packages:** Note that having packages installed does not mean that they are ready to be used. For this you must *load* packages.

Loading may be done by checking the boxes located on the left of the package name in the **Packages** tab or by calling the package through the library() function. If we were now to load *zoo* we would use:

``` r
library(zoo)
```

Note that in this case you do NOT need to enclose the package name in apostrophes.

### Excercise 5

1.  Check if the following packages are installed: graphics, dplyr, raster, devtools, hexbin.
2.  If they are not installed, install the package
3.  Load only the packages you have installed

------------------------------------------------------------------------

<a name = "help"><a/>Getting Help
---------------------------------

There is a great amount of online resources that may help you with R. Some popular websites include [QuickR](http://www.statmethods.net) and [Inside-r](http://www.inside-r.org/).

Furthermore, R also has a repository of help vignettes that can be called upon by using the help function. If you wished to visualize the help vignette for the column bind function you would type :

``` r
?cbind
```

This should open the help vignette on the **Help** tab in the bottom-right window.

### Exercise 6

1.  Ask R for help for the following functions: sum, mean, var, class.

Congratulations! You are know ready to start working with R.

------------------------------------------------------------------------

                                                     [NEXT: DATA](2_data.Rmd)
