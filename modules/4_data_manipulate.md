Introduction to R | Data Manipulation
================
EcoHealth Alliance

<img src = "rlogo.png" style="position:absolute;top:0px;left:0px;"/>

Contents
--------

[Drop or add columns](#drop)

[Data summary](#dsum)

[Change column/row names](#colname)

[Subsetting the dataframe](#subset)

<a name = "drop"><a/> Drop or add columns
-----------------------------------------

More often than not, dataframes are not structured in a way that is most practical for our analyses. Handling large dataframes may be complicated, data might lack information that we need, etc. We are able to perform several manipulations to dataframes to make handling data more convenient.

**Dropping columns** Large dataframes may be troublesome to handle, and may hold information that is not necessary for our particular analyses. We can easily select columns we wish to delete to make our dataframe more manageable.

We can modify the dataframe by specifying columns we wish to retain. Let's continue working with the cgd data frame from the survival package.

    ## Warning: package 'survival' was built under R version 3.3.3

``` r
cgd.drop = cgd[,2:8] # Create new dataframe with columns 2-8 only

head(cgd.drop)       #Remember to create a new object so you don't lose your original data
```

    ##              center     random   treat    sex age height weight
    ## 1 Scripps Institute 1989-06-07  rIFN-g female  12    147   62.0
    ## 2 Scripps Institute 1989-06-07  rIFN-g female  12    147   62.0
    ## 3 Scripps Institute 1989-06-07  rIFN-g female  12    147   62.0
    ## 4 Scripps Institute 1989-06-07 placebo   male  15    159   47.5
    ## 5 Scripps Institute 1989-06-07 placebo   male  15    159   47.5
    ## 6 Scripps Institute 1989-06-07 placebo   male  15    159   47.5

Another way to do this is by specifying which column is to be dropped preceded by the *minus* (-) sign as follows:

``` r
cgd.drop = cgd[,-1]    # New dataframe without the first column 

names(cgd.drop)        # Print column names of the new dataframe
```

    ##  [1] "center"   "random"   "treat"    "sex"      "age"      "height"  
    ##  [7] "weight"   "inherit"  "steroids" "propylac" "hos.cat"  "tstart"  
    ## [13] "enum"     "tstop"    "status"

**Adding columns** : Other times we might want to add information to a dataframe. This is done with the \``cbind` function.

Let's assume we wish to add an ID number for each row in the dataframe:

``` r
IDnumber = 1:nrow(cgd)    # Create a vector with as many elements as there rows in the dataframe

names(cgd)                       # Check column names before adding IDnumber
```

    ##  [1] "id"       "center"   "random"   "treat"    "sex"      "age"     
    ##  [7] "height"   "weight"   "inherit"  "steroids" "propylac" "hos.cat" 
    ## [13] "tstart"   "enum"     "tstop"    "status"

``` r
cgd.add = cbind(IDnumber, cgd)   # Add ID column

names(cgd.add)                   # Column names after adding IDnumber
```

    ##  [1] "IDnumber" "id"       "center"   "random"   "treat"    "sex"     
    ##  [7] "age"      "height"   "weight"   "inherit"  "steroids" "propylac"
    ## [13] "hos.cat"  "tstart"   "enum"     "tstop"    "status"

Keep in mind that the order in which you enter the elements in the `cbind()` function will determine where the column is added.

``` r
cgd.add2 = cbind(cgd, IDnumber)

names(cgd.add2)                  #IDnumber is now the last column in the dataframe
```

    ##  [1] "id"       "center"   "random"   "treat"    "sex"      "age"     
    ##  [7] "height"   "weight"   "inherit"  "steroids" "propylac" "hos.cat" 
    ## [13] "tstart"   "enum"     "tstop"    "status"   "IDnumber"

### EXCERCISE 3

1.  Drop the following columns from the iris dataframe : Sepal.Width, Petal.Width

2.  Add a column with IDnumber to the iris dataframe

------------------------------------------------------------------------

<a name = "colname"><a/>Change column/row names
-----------------------------------------------

Column and row names can be changed with `colnames()` and `rownames()` respectively.

``` r
cgd.head = head(cgd[1:5])  # New data frame with only first 6 rows

colnames(cgd.head) = c("col1", "col2", "col3", "col4", "col5")    # Change column names

rownames(cgd.head) = c("ID1", "ID2", "ID3", "ID4", "ID5", "ID6") # Change row names

cgd.head #print dataframe
```

    ##     col1              col2       col3    col4   col5
    ## ID1    1 Scripps Institute 1989-06-07  rIFN-g female
    ## ID2    1 Scripps Institute 1989-06-07  rIFN-g female
    ## ID3    1 Scripps Institute 1989-06-07  rIFN-g female
    ## ID4    2 Scripps Institute 1989-06-07 placebo   male
    ## ID5    2 Scripps Institute 1989-06-07 placebo   male
    ## ID6    2 Scripps Institute 1989-06-07 placebo   male

You can also change the name of a particular column by specifying its number

``` r
colnames(cgd.head)[2]  = "NewColName" # Specifiy the number of the column being renamed

names(cgd.head)                       # Print new column names
```

    ## [1] "col1"       "NewColName" "col3"       "col4"       "col5"

------------------------------------------------------------------------

<a name = "subset"><a/>Subsetting the dataframe
-----------------------------------------------

There may be times when we might want to manipulate smaller sets of the original dataframe. For example we may be interested only in those entries where patients younger than 20 years of age.

``` r
cgdU20 = cgd[cgd$age < 20,]             # Get all rows with age smaller than 20
                                        # The comma is important here

summary(cgdU20$age)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##   1.000   5.000   8.000   9.047  13.000  19.000

Or we might be interested only in a specific treatment

``` r
Placebo = cgd[cgd$Streat == "placebo",]     # Get all rows with treat = placebo 
                                            # The comma is important here

head(Placebo$treat)                         # Print first values of the dataframe
```

    ## factor(0)
    ## Levels: placebo rIFN-g

However if we use *str*() we will notice that the other levels for treatment have been retained. This happens because Status is a *factor*.

``` r
str(Placebo)
```

    ## 'data.frame':    0 obs. of  16 variables:
    ##  $ id      : int 
    ##  $ center  : Factor w/ 13 levels "Harvard Medical Sch",..: 
    ##  $ random  :Class 'Date'  num(0) 
    ##  $ treat   : Factor w/ 2 levels "placebo","rIFN-g": 
    ##  $ sex     : Factor w/ 2 levels "male","female": 
    ##  $ age     : int 
    ##  $ height  : num 
    ##  $ weight  : num 
    ##  $ inherit : Factor w/ 2 levels "X-linked","autosomal": 
    ##  $ steroids: num 
    ##  $ propylac: num 
    ##  $ hos.cat : Factor w/ 4 levels "US:NIH","US:other",..: 
    ##  $ tstart  : int 
    ##  $ enum    : int 
    ##  $ tstop   : int 
    ##  $ status  : int

To successfully subset dataframes by factors we must use *droplevels*().

``` r
Placebo = droplevels(cgd[cgd$treat == "placebo",]) #The comma is important
str(Placebo)
```

    ## 'data.frame':    120 obs. of  16 variables:
    ##  $ id      : int  2 2 2 2 2 2 2 2 5 5 ...
    ##  $ center  : Factor w/ 13 levels "Harvard Medical Sch",..: 2 2 2 2 2 2 2 2 4 4 ...
    ##  $ random  : Date, format: "1989-06-07" "1989-06-07" ...
    ##  $ treat   : Factor w/ 1 level "placebo": 1 1 1 1 1 1 1 1 1 1 ...
    ##  $ sex     : Factor w/ 2 levels "male","female": 1 1 1 1 1 1 1 1 1 1 ...
    ##  $ age     : int  15 15 15 15 15 15 15 15 17 17 ...
    ##  $ height  : num  159 159 159 159 159 ...
    ##  $ weight  : num  47.5 47.5 47.5 47.5 47.5 47.5 47.5 47.5 52.7 52.7 ...
    ##  $ inherit : Factor w/ 2 levels "X-linked","autosomal": 2 2 2 2 2 2 2 2 1 1 ...
    ##  $ steroids: num  0 0 0 0 0 0 0 0 0 0 ...
    ##  $ propylac: num  1 1 1 1 1 1 1 1 1 1 ...
    ##  $ hos.cat : Factor w/ 4 levels "US:NIH","US:other",..: 2 2 2 2 2 2 2 2 1 1 ...
    ##  $ tstart  : int  0 8 26 152 241 249 322 350 0 246 ...
    ##  $ enum    : int  1 2 3 4 5 6 7 8 1 2 ...
    ##  $ tstop   : int  8 26 152 241 249 322 350 439 246 253 ...
    ##  $ status  : int  1 1 1 1 1 1 1 0 1 1 ...

Furthermore, we can exclude rows with certain values by using logical operators. For example, we will retrieve all entries where the patient is not female.

``` r
cgd.male = droplevels(cgd[cgd$sex != "female",])  # Get all rows with sex different from female
                                                  # != means different than
summary(cgd.male$sex)
```

    ## male 
    ##  168

### EXCERCISE 4

Using the *iris* dataframe create different subsets for:

1.  All flowers with petals 4mm or longer

2.  Flowers with petal widths smaller than 1mm

3.  All species except *virginica*

### Operations with dataframes

R also allows us to perform calculations on specific dataframe columns. For example, let's convert *height* so it is represented in meters instead of centimeters.

``` r
cgd$height = cgd$height/100   #convert from centimeters to meters 

print(head(cgd$height))
```

    ## [1] 1.47 1.47 1.47 1.59 1.59 1.59

We can also create new columns and add them to the dataframe by performing operations between 2 or more columns. For example, we will calculate the Body Mass Index (BMI) and add this new variable to the *cgd* dataframe.

``` r
cgd$BMI = cgd$weight/((cgd$height*100)^2) #BMI = Kg/cm^2 

print(head(cgd))
```

    ##   id            center     random   treat    sex age height weight
    ## 1  1 Scripps Institute 1989-06-07  rIFN-g female  12   1.47   62.0
    ## 2  1 Scripps Institute 1989-06-07  rIFN-g female  12   1.47   62.0
    ## 3  1 Scripps Institute 1989-06-07  rIFN-g female  12   1.47   62.0
    ## 4  2 Scripps Institute 1989-06-07 placebo   male  15   1.59   47.5
    ## 5  2 Scripps Institute 1989-06-07 placebo   male  15   1.59   47.5
    ## 6  2 Scripps Institute 1989-06-07 placebo   male  15   1.59   47.5
    ##     inherit steroids propylac  hos.cat tstart enum tstop status
    ## 1 autosomal        0        0 US:other      0    1   219      1
    ## 2 autosomal        0        0 US:other    219    2   373      1
    ## 3 autosomal        0        0 US:other    373    3   414      0
    ## 4 autosomal        0        1 US:other      0    1     8      1
    ## 5 autosomal        0        1 US:other      8    2    26      1
    ## 6 autosomal        0        1 US:other     26    3   152      1
    ##           BMI
    ## 1 0.002869175
    ## 2 0.002869175
    ## 3 0.002869175
    ## 4 0.001878881
    ## 5 0.001878881
    ## 6 0.001878881

### EXERCISE 5

1.  Convert Sepal.Length from *mm* to *cm*
2.  Create a new column *Petal.Ratio* by calculating Petal length divided by width \*\*\*

<a name = "dsum"><a/>Data summary
---------------------------------

Something that could be quite useful to provide a better understanding of our data is to get a quick statistical summary of our dataframe.

``` r
summary(cgd)
```

    ##        id                          center       random          
    ##  Min.   :  1.00   NIH                 :41   Min.   :1989-06-07  
    ##  1st Qu.: 24.50   Scripps Institute   :36   1st Qu.:1989-08-19  
    ##  Median : 54.00   Amsterdam           :28   Median :1989-09-15  
    ##  Mean   : 58.09   Univ. of Zurich     :21   Mean   :1989-09-22  
    ##  3rd Qu.: 89.50   Mott Children's Hosp:20   3rd Qu.:1989-11-03  
    ##  Max.   :135.00   L.A. Children's Hosp:13   Max.   :1989-12-29  
    ##                   (Other)             :44                       
    ##      treat         sex           age           height     
    ##  placebo:120   male  :168   Min.   : 1.0   Min.   :0.763  
    ##  rIFN-g : 83   female: 35   1st Qu.: 6.0   1st Qu.:1.145  
    ##                             Median :12.0   Median :1.400  
    ##                             Mean   :13.7   Mean   :1.381  
    ##                             3rd Qu.:20.0   3rd Qu.:1.692  
    ##                             Max.   :44.0   Max.   :1.890  
    ##                                                           
    ##      weight            inherit       steroids          propylac     
    ##  Min.   : 10.40   X-linked :131   Min.   :0.00000   Min.   :0.0000  
    ##  1st Qu.: 20.25   autosomal: 72   1st Qu.:0.00000   1st Qu.:1.0000  
    ##  Median : 33.40                   Median :0.00000   Median :1.0000  
    ##  Mean   : 39.34                   Mean   :0.03448   Mean   :0.8473  
    ##  3rd Qu.: 58.70                   3rd Qu.:0.00000   3rd Qu.:1.0000  
    ##  Max.   :101.50                   Max.   :1.00000   Max.   :1.0000  
    ##                                                                     
    ##              hos.cat        tstart           enum           tstop      
    ##  US:NIH          : 41   Min.   :  0.0   Min.   :1.000   Min.   :  4.0  
    ##  US:other        :108   1st Qu.:  0.0   1st Qu.:1.000   1st Qu.:204.5  
    ##  Europe:Amsterdam: 28   Median :  0.0   Median :1.000   Median :273.0  
    ##  Europe:other    : 26   Mean   : 69.5   Mean   :1.665   Mean   :254.1  
    ##                         3rd Qu.:121.0   3rd Qu.:2.000   3rd Qu.:320.0  
    ##                         Max.   :373.0   Max.   :8.000   Max.   :439.0  
    ##                                                                        
    ##      status            BMI          
    ##  Min.   :0.0000   Min.   :0.001237  
    ##  1st Qu.:0.0000   1st Qu.:0.001616  
    ##  Median :0.0000   Median :0.001762  
    ##  Mean   :0.3744   Mean   :0.001890  
    ##  3rd Qu.:1.0000   3rd Qu.:0.002096  
    ##  Max.   :1.0000   Max.   :0.008321  
    ## 

The `summary()` function allows us to explore the number of counts and labels for categorical data and provides information on the distribution of continuous variables (e.g. min, max, mean)

### EXCERCISE 6

1.  Summarize the *iris* dataframe
2.  What is the maximum Petal length?
3.  How many individuals of the *setosa* species are there?
