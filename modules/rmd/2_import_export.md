Introduction to R | Importing and Exporting data files
================
EcoHealth Alliance

<img src = "rlogo.png" style="position:absolute;top:0px;left:0px;"/>

Contents
--------

[Quick intro to variables](#varintro)

[**Importing**](#imp)

[CSV files](#icsv)

[TXT files](#itxt)

[Excel spreadsheet](#ixls)

[SPSS](#ispss)

[SAS](#isas)

[Stata](#istata)

[\***Viewing data**](#view)

[**Exporting**](#exp)

[CSV files](#ecsv)

[TXT files](#etxt)

[Excel spreadsheet](#exls)

[SPSS](#espss)

[SAS](#esas)

[Stata](#estata)

<a name = "varintro"><a/>Quick intro to variables
-------------------------------------------------

Variables are names we assign to a value or set of values to be stored an manipulated in R.

These values can be numeric:

``` r
x = 10    # assign a value to x
y = 2     # assign a value to y

x         # print x
```

    ## [1] 10

Or characters (letters/strings):

``` r
Name = "Susan"

print(Name)
```

    ## [1] "Susan"

We can also assign a variable name to an array of values (vectors). Vectors can also be numerics or characters:

``` r
# a numeric vector
numer = c(1,2,3) #the letter c before the parenthesis is the "concatenate" function

# a character (string/letters) vector
alpha = c("a", "b", "c")

print(numer)
```

    ## [1] 1 2 3

``` r
print(alpha)
```

    ## [1] "a" "b" "c"

Note that all elements within a vector must belong to the same class. Let's see what happens when we create a vector with both numeric and character elements.

``` r
alphanumer = c(1, "a", "b")

print(alphanumer)
```

    ## [1] "1" "a" "b"

``` r
class(alphanumer)
```

    ## [1] "character"

The number 1 has been converted to a character ("1"). This means that it is no longer recognized as a numeric and cannot be used to perform mathematical operations.

We can even assing variable names to a group a of vectors such as matrices.

``` r
# create 2 vectors
numer = c(1,2,3)
numer2 = c(4,5,6)
alpha = c("a", "b", "c")

#join the 2 numeric vectors into a matrix
A = matrix(c(numer, numer2), nrow =2)
print(A)
```

    ##      [,1] [,2] [,3]
    ## [1,]    1    3    5
    ## [2,]    2    4    6

Or a dataframe:

``` r
# join these 3 vectors in a single data frame
df = data.frame(numer, numer2, alpha)

print(df)
```

    ##   numer numer2 alpha
    ## 1     1      4     a
    ## 2     2      5     b
    ## 3     3      6     c

The main difference between matrices and dataframes is that the latter allow us to group different data types into a single table while all elements in a matrix, just like vectors, must belong to the same class. Usually the data we collect and analyze is in dataframe format.

Now that we have a basic understanding of variables, we will learn how we can import data tables from other sources and assign variables to them.

<a name = "imp"><a/>Importing
-----------------------------

Many times the data we collect is stored in other formats (e.g. CSV, SAS, Excel) and we may need to import it for analysis in R. When we import data tables into R they create dataframe objects.

### <a name = "icsv"><a/>CSV files

To import csv files we can use the `read.csv()` function.

``` r
csv = read.csv("MyData.csv", header= TRUE, sep = ",")
```

Note that `header = TRUE` indicates that the first row of the dataframe should not be considered as part of the data since it holds variable names. If this is not the case for your data then you would set `header = FALSE`.

The `sep` parameter indicates the delimiter to be recognized as separator between columns in your data. Since this is a **comma separated value** (csv) file, we should set *comma* (,) as the delimiter by inputing `sep = ","`.

### <a name = "itxt"><a/>TXT files

Flat text files can be imported into R using `read.table()`

``` r
txt = read.table("MyData.txt", header = TRUE, sep = "\t")
```

`read.table()` is a generalized version of `read.csv()` and can also be used to import CSV files. In this case the data is tabulated (columns separated by tab) so we set `sep = "\t"` as the delimiter.

### <a name = "ixls"><a/>Excel spreadsheet

Before being able to import excel files, we must first load the *xlsx* library

``` r
library(readxl)
excel1 = as.data.frame(read_xlsx("MyData.xlsx", sheet = 1, col_names = TRUE))
```

The `sheet = 1` parameter is indicating that the first sheet of the workbook is to be imported as a dataframe. If you wish to load information from another sheet you may either indicate its index or alternatively its name.

``` r
excel2 = as.data.frame(read_xlsx("MyData.xlsx", sheet = "Sheet2", col_names = TRUE))
```

The `col_names` parameter indicates whether the first row of the dataframe contains variable names/labels (TRUE) or not (FALSE).

### <a name = "ispss"><a/>SPSS

R can import SPSS data sets with the `read_._spss()` function from the *haven* package.

``` r
# Load the foreign package
library(haven)
spss1 = read_spss("MyData.sav", user_na = FALSE)
```

Alternatively, we can use the `spss.get()` function from the *Hmisc* package.

``` r
install.packages("Hmisc") #if not previously installed
library(Hmisc)
spss2 = spss.get("MyData.sav", use.value.label = TRUE)
```

`use.value.label = TRUE` converts all variables with labels in SPSS into factors in R.

### <a name = "isas"><a/>SAS

There are different ways in which you can import SAS files into R, however the most convenient is to export your SAS dataset into CSV and then import it using the `read.csv()` function as mentioned previously.

Another way you can import your SAS data is by using the `read_sas()` function from the *haven* library.

``` r
sas = read_sas("MyData.xpt")
```

### <a name = "istata"><a/>Stata

To import Stata files we will also use the *haven* package and its `read_stata()`function.

``` r
library(foreign)
stata = read_dta("MyData.dta")
```

------------------------------------------------------------------------

### <a name = "view"><a/>Viewing data

Once our data is loaded to the R environment, we can take a quick look at these as a table

``` r
view(sas)
```

We can also do this by double-clicking on the R object in the *Environment* tab in the upper right window of **RStudio**.

------------------------------------------------------------------------

<a name = "exp"><a/> Exporting
------------------------------

Exporting dataframes or result tables from R to other formats is also possible.

### <a name = "ecsv"><a/>CSV files

Exporting csv files from R can be done using the `write.csv()` function.

``` r
write.csv(data, file = "MyData.csv")
```

Note that by default your files will be saved in your working directory. If you wish to save these somewhere else you **must** specify the file path. For example:

``` r
write.csv(data, file = "C:/MyFilePath/MyData.csv")
```

### <a name = "etxt"><a/>TXT

Exporting a generic txt file is similar to exporting csv files. In this case we will use the `write.table()` command.

``` r
write.table(data, file = "MyData.txt", sep = "\t")
```

Note that we have set `sep = "\t"` and thus created a tabulated file. We could have created a csv file by setting the `sep = ","`.

### <a name = "exls"><a/>Excel spreadsheet

To export dataframes to excel spreadsheets we must load the *xlsx* package.

``` r
library(xlsx)
write.xlsx(csv, "MyData.xlsx")
```

### <a name = "ispss"><a/>SPSS

As with importing, the *haven* library is necessary to export SPSS file via its `write_sav()` function.

``` r
write_sav(csv, path = "MyData.sps")
```

### <a name = "isas"><a/>SAS

The `write_sas()` function from *haven* can also be used to export dataframes in SAS format in a similar way to SPSS files.

``` r
write_sas(csv, path = "MyData.sas")
```

### <a name = "istata"><a/>Stata

The *haven* package is also required to export Stata files. `write_dta()` can be used to export dataframes in Stata binary format

``` r
write_dta(csv, "MyData.dta")
```
