Introduction to R | Data
================
EcoHealth Alliance

<img src = "rlogo.png" style="position:absolute;top:0px;left:0px;"/>

Contents
--------

[Dataframes](#df)

[Dataframe structure](#str)

[Numerics & Integers](#numint)

[Factors & Characters](#char)

[Vectors](#vec)

<a name = "df"><a/>Dataframes
-----------------------------

We have learned how to load dataframes. Now we will explore the general structure of our data and what types of variables it contains.

The first row in a dataframe is called the *header* and holds all column (variable) names. The first column of the dataframe usually consists of row names. However, row names aren't always present in dataframes. All rows after the *header* are called *data rows*. Each member of a row is called a *cell*.

We will start by loading the *cgd* (Chronic Granulotomous Disease data) dataset built into the *survival* package.package.

    ## Warning: package 'survival' was built under R version 3.3.3

We can quickly look at the number of rows in our dataframe

``` r
nrow(cgd)    # Number of rows in cgd
```

    ## [1] 203

Likewise we can look at the number of columns, or in this case variables

``` r
ncol(cgd) # Number of variables in cgd
```

    ## [1] 16

If we want to get a general idea of what our dataframe looks like, we can take a look at its first (head) entries

``` r
head(cgd) # First 6 elements
```

    ##   id            center     random   treat    sex age height weight
    ## 1  1 Scripps Institute 1989-06-07  rIFN-g female  12    147   62.0
    ## 2  1 Scripps Institute 1989-06-07  rIFN-g female  12    147   62.0
    ## 3  1 Scripps Institute 1989-06-07  rIFN-g female  12    147   62.0
    ## 4  2 Scripps Institute 1989-06-07 placebo   male  15    159   47.5
    ## 5  2 Scripps Institute 1989-06-07 placebo   male  15    159   47.5
    ## 6  2 Scripps Institute 1989-06-07 placebo   male  15    159   47.5
    ##     inherit steroids propylac  hos.cat tstart enum tstop status
    ## 1 autosomal        0        0 US:other      0    1   219      1
    ## 2 autosomal        0        0 US:other    219    2   373      1
    ## 3 autosomal        0        0 US:other    373    3   414      0
    ## 4 autosomal        0        1 US:other      0    1     8      1
    ## 5 autosomal        0        1 US:other      8    2    26      1
    ## 6 autosomal        0        1 US:other     26    3   152      1

or last (tail) ones

``` r
tail(cgd) # Last 6 elements
```

    ##      id               center     random   treat    sex age height weight
    ## 198 132 L.A. Children's Hosp 1989-12-25 placebo female   7  113.0   20.4
    ## 199 132 L.A. Children's Hosp 1989-12-25 placebo female   7  113.0   20.4
    ## 200 133 L.A. Children's Hosp 1989-12-28  rIFN-g   male  15  178.7   60.5
    ## 201 134    Scripps Institute 1989-12-29 placebo female   6  130.0   21.6
    ## 202 134    Scripps Institute 1989-12-29 placebo female   6  130.0   21.6
    ## 203 135    Scripps Institute 1989-12-29 placebo female   3   96.0   13.1
    ##       inherit steroids propylac  hos.cat tstart enum tstop status
    ## 198 autosomal        0        1 US:other      0    1   120      1
    ## 199 autosomal        0        1 US:other    120    2   203      0
    ## 200  X-linked        0        1 US:other      0    1   197      0
    ## 201 autosomal        0        1 US:other      0    1   104      1
    ## 202 autosomal        0        1 US:other    104    2   227      0
    ## 203 autosomal        0        1 US:other      0    1   227      0

We can also determine the value of a particular cell by specifying the row and column number from which we wish to extract values.

``` r
cgd[2,3]   # Value from second row and third column
```

    ## [1] "1989-06-07"

Additionally, we can find out how many elements are within a single column of the dataframe

``` r
length(cgd$center) #should be the same as nrow
```

    ## [1] 203

### EXERCISE 1

1.  Load the in-built *iris* dataframe
2.  How many rows are in this dataframe?
3.  Get the first 6 elements of the dataframe

<a name = "str"><a/> Dataframe structure
----------------------------------------

We can also check the structure of our dataframe

``` r
#Visualize the structure of the dataframe using the str() function

str(cgd)
```

    ## 'data.frame':    203 obs. of  16 variables:
    ##  $ id      : int  1 1 1 2 2 2 2 2 2 2 ...
    ##  $ center  : Factor w/ 13 levels "Harvard Medical Sch",..: 2 2 2 2 2 2 2 2 2 2 ...
    ##  $ random  : Date, format: "1989-06-07" "1989-06-07" ...
    ##  $ treat   : Factor w/ 2 levels "placebo","rIFN-g": 2 2 2 1 1 1 1 1 1 1 ...
    ##  $ sex     : Factor w/ 2 levels "male","female": 2 2 2 1 1 1 1 1 1 1 ...
    ##  $ age     : int  12 12 12 15 15 15 15 15 15 15 ...
    ##  $ height  : num  147 147 147 159 159 159 159 159 159 159 ...
    ##  $ weight  : num  62 62 62 47.5 47.5 47.5 47.5 47.5 47.5 47.5 ...
    ##  $ inherit : Factor w/ 2 levels "X-linked","autosomal": 2 2 2 2 2 2 2 2 2 2 ...
    ##  $ steroids: num  0 0 0 0 0 0 0 0 0 0 ...
    ##  $ propylac: num  0 0 0 1 1 1 1 1 1 1 ...
    ##  $ hos.cat : Factor w/ 4 levels "US:NIH","US:other",..: 2 2 2 2 2 2 2 2 2 2 ...
    ##  $ tstart  : int  0 219 373 0 8 26 152 241 249 322 ...
    ##  $ enum    : int  1 2 3 1 2 3 4 5 6 7 ...
    ##  $ tstop   : int  219 373 414 8 26 152 241 249 322 350 ...
    ##  $ status  : int  1 1 0 1 1 1 1 1 1 1 ...

We can now visualize the number of observations (203) and variables (16) in this dataframe. Likewise, we can see the first elements for each variable (column) and the data class to which it belongs to. In this case we have 4 types of data *integers* (e.g. id, age), *numerics* (e.g. height, weight), *factors* (e.g. treatment, sex) and *date*.

### EXERCISE 2

1.  Load the built-in *iris* dataframe using the `data()` function.
2.  Check the structure of this dataframe
3.  What types of variables does it contain?

We will now talk about the different types of data R deals with

------------------------------------------------------------------------

<a name = "numint"><a/> Numeric & integer variables
---------------------------------------------------

R understands *numerics* as numbers with decimals. For example, let's extract the *weight* vector from the *cgd* dataframe.

``` r
weight = cgd$weight

class(weight) #The class function tells us what data type we are dealing with
```

    ## [1] "numeric"

When using the `class()` function, we can observe that *weight* is indeed a numeric type variable. However, what happens when we do the same with the *age* vector?

``` r
age = cgd$age
class(age)
```

    ## [1] "integer"

We see that even though *age* is also a number, it is classified as a *integer* variable. Non-decimal variables are called *integers*.

We can transform these integer values into numeric (with decimals) by calling the `as.numeric()` function.

``` r
age_num = as.numeric(age)
class(age_num)
```

    ## [1] "numeric"

We can also coerce numeric values into integer variables by using the `as.integer()` function.

``` r
weight_int = as.integer(weight)  # Transform from numeric to integer

class(weight_int)                # Get new integer vector
```

    ## [1] "integer"

Note that R coerces numeric variables into integers by deleting any decimals or *rounding down*.

``` r
print(weight_int)
```

    ##   [1]  62  62  62  47  47  47  47  47  47  47  47  72  34  52  52  52  45
    ##  [18]  59  59  17  82  82  19  13  13  25  25  36  10  10  10  10  10  10
    ##  [35]  32  32  32  32  67  33  33  33  11  11  50  73  73  51  19  46  30
    ##  [52]  23  23  10  13  14  18  18  12  12  15  15  15  67  49  31  59  36
    ##  [69]  36  36  13  68  80  23  47  47  47  27  61  68  68  36  63  63  46
    ##  [86]  50  29  29  29  74  74  34  68  68  68  68  23  23  23  23  23  66
    ## [103]  28  28  52  65  65  65  65  95  23  19  29  29  19  19  19  15  15
    ## [120]  66  66  78  31  31  34  49  17  31  31  27  49  49  13  20  22  24
    ## [137]  32  94  73  73  14  21  10  22  29  46  16  16  71  71  19  20  36
    ## [154]  36  28  50  58  20  26  34  19  14  14  14  14  58  42  42  11  58
    ## [171]  80  24  55  51  27  63  55  20  20  69  36  36  31  74 101  40  17
    ## [188]  14  14  14  14  49  63  63  63  60  67  20  20  60  21  21  13

Keep in mind that the default for R is to interpret numbers as numerics. So when you import a dataframe from another source integer values will be assumed to be numeric, that is having decimal values.

### EXERCISE 3

1.  Extract the *Petal.Length* column into an independent vector called *PetalLen*
2.  Determine what data type this new vector is using the `class()` function.
3.  Coerce this vector into an integer

------------------------------------------------------------------------

<a name = "char"><a/> Factors & Characters
------------------------------------------

Factors are categorical variables, meaning that they can only take a limited number of different values. For example, in the *sex* column of the *cgd * dataframe, we only observe 2 possible categories, male and female.

``` r
class(cgd$sex)
```

    ## [1] "factor"

``` r
levels(cgd$sex)
```

    ## [1] "male"   "female"

Though dealing with a limited categories is useful, however as the number of these category levels increase it may become unmanageable. In that case we may prefer working with character variables. These are string (or letter) values, however they are not restricted to a limited number of categories. Like factors, Character strings are also enclosed in quotations (`" "`).

We can easily convert factors into characters with the `as.character()` function. Let's do it for the *center* column within the *cgd* dataframe:

``` r
cgd$center = as.character(cgd$center)

class(cgd$center)
```

    ## [1] "character"

Note that by using the **$** operator we are not creating a new vector as we had done previously, rather we are choosing the column (center) within the dataframe (cgd) and applying these changes directly to the dataframe. Such that:

``` r
str(cgd)
```

    ## 'data.frame':    203 obs. of  16 variables:
    ##  $ id      : int  1 1 1 2 2 2 2 2 2 2 ...
    ##  $ center  : chr  "Scripps Institute" "Scripps Institute" "Scripps Institute" "Scripps Institute" ...
    ##  $ random  : Date, format: "1989-06-07" "1989-06-07" ...
    ##  $ treat   : Factor w/ 2 levels "placebo","rIFN-g": 2 2 2 1 1 1 1 1 1 1 ...
    ##  $ sex     : Factor w/ 2 levels "male","female": 2 2 2 1 1 1 1 1 1 1 ...
    ##  $ age     : int  12 12 12 15 15 15 15 15 15 15 ...
    ##  $ height  : num  147 147 147 159 159 159 159 159 159 159 ...
    ##  $ weight  : num  62 62 62 47.5 47.5 47.5 47.5 47.5 47.5 47.5 ...
    ##  $ inherit : Factor w/ 2 levels "X-linked","autosomal": 2 2 2 2 2 2 2 2 2 2 ...
    ##  $ steroids: num  0 0 0 0 0 0 0 0 0 0 ...
    ##  $ propylac: num  0 0 0 1 1 1 1 1 1 1 ...
    ##  $ hos.cat : Factor w/ 4 levels "US:NIH","US:other",..: 2 2 2 2 2 2 2 2 2 2 ...
    ##  $ tstart  : int  0 219 373 0 8 26 152 241 249 322 ...
    ##  $ enum    : int  1 2 3 1 2 3 4 5 6 7 ...
    ##  $ tstop   : int  219 373 414 8 26 152 241 249 322 350 ...
    ##  $ status  : int  1 1 0 1 1 1 1 1 1 1 ...

We can see that that the class for *center* has changed.

### EXERCISE 4

1.  Transform the *Species* column into a character vector.
