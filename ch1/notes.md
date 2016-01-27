
Also useful, R for Octave users: https://cran.r-project.org/doc/contrib/R-and-octave.txt

# Kelly Black's R tute 
http://www.cyclismo.org/tutorial/R/index.html


## read csv

* get in and get summary info
```R
> tree <- read.csv(file="trees91.csv",header=TRUE,sep=",");
> names(tree)
 [1] "C"      "N"      "CHBR"   "REP"    "LFBM"   "STBM"   "RTBM"   "LFNCC" 
 [9] "STNCC"  "RTNCC"  "LFBCC"  "STBCC"  "RTBCC"  "LFCACC" "STCACC" "RTCACC"
[17] "LFKCC"  "STKCC"  "RTKCC"  "LFMGCC" "STMGCC" "RTMGCC" "LFPCC"  "STPCC" 
[25] "RTPCC"  "LFSCC"  "STSCC"  "RTSCC" 
> attributes(tree)
$names
 [1] "C"      "N"      "CHBR"   "REP"    "LFBM"   "STBM"   "RTBM"   "LFNCC" 
 [9] "STNCC"  "RTNCC"  "LFBCC"  "STBCC"  "RTBCC"  "LFCACC" "STCACC" "RTCACC"
[17] "LFKCC"  "STKCC"  "RTKCC"  "LFMGCC" "STMGCC" "RTMGCC" "LFPCC"  "STPCC" 
[25] "RTPCC"  "LFSCC"  "STSCC"  "RTSCC" 

$class
[1] "data.frame"

$row.names
 [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25
[26] 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40 41 42 43 44 45 46 47 48 49 50
[51] 51 52 53 54
```
* get column

```R
> tree$C
 [1] 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 3 3 3 3 3 3 3
[39] 3 3 3 4 4 4 4 4 4 4 4 4 4 4 4 4
```

## data types

### variables, vectors

* numbers, work how you'd expect
```R
> a <- 3
> a
[1] 3
```
* interestingly,
```R
> ':' (0,5)
[1] 0 1 2 3 4 5
> '+' (1,2)
[1] 3
```
* vectors
 * indexing starts at 1, not 0
```R
> bubba <- c(3,5,7,9)
> bubba
[1] 3 5 7 9
> bubba[1]
[1] 3
```
 * zero index is used for data type
```R
> bubba[0]
numeric(0
> b <- c('a','b','c')
> b[0]
character(0)
> typeof(b)
[1] "character"
```
 * can index with logicals 
```R
> a <- c(1,2,3,4,5)
> b <- c(TRUE,FALSE,FALSE,TRUE,FALSE)
> a[b]
[1] 1 4
> a[a<6]
```
 * can do basic operations with them
```R
> mean(bubba)
[1] 6
> bubba+1
[1]  4  6  8 10
```

### factors

* a factor is different categories or levels of something
* if entries are not numbers, R assumes it is a factor
```R
> tree$CHBR
 [1] CL6 CL7 A1  A1  A1  A7  A3  D5  A4  A4  A4  B3  B3  B3  B6  B6  B6  A5  B4 
[20] B4  B4  B7  B7  B7  A2  A6  A6  A6  B5  B5  B5  B1  B2  B2  B2  D2  C1  C2 
[39] C2  C2  D1  C4  C4  C4  C7  D6  C5  D3  D3  D3  D7  C3  C6  D4 
30 Levels: A1 A2 A3 A4 A5 A6 A7 B1 B2 B3 B4 B5 B6 B7 C1 C2 C3 C4 C5 C6 ... D7
> summary(tree$CHBR)
 A1  A2  A3  A4  A5  A6  A7  B1  B2  B3  B4  B5  B6  B7  C1  C2  C3  C4  C5  C6 
  3   1   1   3   1   3   1   1   3   3   3   3   3   3   1   3   1   3   1   1 
 C7 CL6 CL7  D1  D2  D3  D4  D5  D6  D7 
  1   1   1   1   1   3   1   1   1   1 
```
* if you've got a column with numbers representing factors, you can use the `factor` command to let R know
```
> tree$C
 [1] 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 3 3 3 3 3 3 3
[39] 3 3 3 4 4 4 4 4 4 4 4 4 4 4 4 4
> tree$C <- factor(tree$C)
> tree$C
 [1] 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 3 3 3 3 3 3 3
[39] 3 3 3 4 4 4 4 4 4 4 4 4 4 4 4 4
Levels: 1 2 3 4
```

### create your own data frame

```R
> a <- c(1,2,3,4)
> b <- c(2,4,6,8)
> levels <- factor(c("A","B","A","B"))
> bubba <- data.frame(first=a,second=b,f=levels)
> bubba
  first second f
1     1      2 A
2     2      4 B
3     3      6 A
4     4      8 B
```

### boolean and operators

* all caps for `TRUE` and `FALSE`, also equiv to 1 and 0
* operators: `<, >, <=, >=, ==, !=, ||, &&, !`
* elementwise: `|, &`
```R
> a <- c(TRUE,FALSE)
> b <- c(TRUE,TRUE)
> a | b
[1] TRUE TRUE
> a & b
[1]  TRUE FALSE
```
* a bunch of test under `is.` e.g. `is.logical`, seems to check the elements rather than the thing itself
```R
> is.logical(a)
[1] TRUE
```

### one way tables

* a table with one row
```R
> a <- factor(c("A","A","B","A","B","B","C","A","C"))
> results <- table(a)
> results
a
A B C 
4 3 2 
```

### two way tables

* an actual table
 * can create by specifying each response itself
```R
> question1 <- c("Sometimes","Sometimes","Never","Always","Always","Sometimes","Sometimes","Never")
> question2 <- c("Maybe","Maybe","Yes","Maybe","Maybe","No","Yes","No")
> results <- table(question1,question2)
> results
           question2
question1   Maybe No Yes
  Always        2  0   0
  Never         0  1   1
  Sometimes     2  1   1
```
 * or could create if you know the totals beforehand
```R
> q1q2 <- matrix(c(2,0,0,0,1,1,2,1,1),ncol=3,byrow=TRUE)
> rownames(q1q2) <- c("always","never","sometimes")
> colnames(q1q2) <- c("maybe","no","yes")
> q1q2
          maybe no yes
always        2  0   0
never         0  1   1
sometimes     2  1   1
```
 * hmph
```R
> typeof(results)
[1] "integer"
> typeof(q1q2)
[1] "double"
> class(results)
[1] "table"
```

## operations

* a vector can have the basic operations on each element with a number: `+, -, *, /`. Also `sqrt(a), exp(a), log(a)`. Also `sum(a), sort(a), min(a)` and so on
```R
> a <- c(1,2,3,4)
> a/4
[1] 0.25 0.50 0.75 1.00
```
* operations between two vectors are performed elementwise
```R
> b
[1] -9 -8 -7 -6
> a*b
[1]  -9 -16 -21 -24
```
* `ls()` will list all the things you've defined in the workspace
* columns of data frames are treated as vectors
```R
> tree$LFBM + 1
 [1] 1.430 1.400 1.450 1.820 1.520 2.320 1.900 2.180 1.480 1.210 1.270 1.310
[13] 1.650 1.180 1.520 1.300 1.580 1.480 1.580 1.580 1.410 1.480 2.760 2.210
[25] 2.180 1.830 2.220 1.770 2.020 1.130 1.680 1.610 1.700 1.820 1.760 1.770
[37] 2.690 2.480 1.740 2.240 2.120 1.750 1.390 1.870 1.410 1.560 1.550 1.670
[49] 2.260 1.965 1.840 1.970 2.070 2.220
```
* `summary()` will give you the quick basic stats, you can apply it to the whole data frame (doing each column individually) like `summary(tree)` or to a particular column
```R
> summary(tree$LFBM)
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
 0.1300  0.4800  0.7200  0.7649  1.0080  1.7600 
```

## probability distributions

* `help(Distributions)` will list what's available
 * `d`: height of pdf
    ```R
    > a <- seq(-1,1,length=10) # Like linspace
    > a
     [1] -1.0000000 -0.7777778 -0.5555556 -0.3333333 -0.1111111  0.1111111
     [7]  0.3333333  0.5555556  0.7777778  1.0000000
    > dnorm(a)
     [1] 0.2419707 0.2948149 0.3418923 0.3773832 0.3964873 0.3964873 0.3773832
     [8] 0.3418923 0.2948149 0.2419707
    > plot(a,dnorm(a))
    ```
 * `p`: height of cdf
    ```R
    > a <- seq(-1,1,by=.1) # -1:.1:1
    > pnorm(a)
     [1] 0.1586553 0.1840601 0.2118554 0.2419637 0.2742531 0.3085375 0.3445783
     [8] 0.3820886 0.4207403 0.4601722 0.5000000 0.5398278 0.5792597 0.6179114
    [15] 0.6554217 0.6914625 0.7257469 0.7580363 0.7881446 0.8159399 0.8413447
    > plot(a,pnorm(a))

    > pnorm(0)
    [1] 0.5
    > pnorm(.1)
    [1] 0.5398278
    > pnorm(.1,lower.tail=FALSE) # 1-pnorm, for the probability it's larger than
    [1] 0.4601722
    ```
 * `q`: inverse cdf, i.e. you give it a probability and it returns the number whose cumulative distribution matches the probability.
    ```R
    > qnorm(0.5)
    [1] 0
    > qnorm(0.5,mean=1)
    [1] 1
    ```
 * `r`: a random number drawn from 
```R
> y <- rnorm(200,mean=-2,sd=4)
> hist(y)
> qqnorm(y)
> qqline(y)
```

### (skipped t-dist, binomial, chi-square)

## plotting 

### basic plots


* some examples
 * `stripchart(w1$vals,method="stack")` v. basic plot of the values as they appear on a line, with multiples stacked
 * `hist(w1$vals,breaks=10,main="Distribution of w1",xlab="w1")` histogram with 10 buckets, title in main, and xlabel
 * `boxplot(w1$vals, main='Leaf BioMass in High CO2 Environment', ylab='BioMass of Leaves')` boxplot obvs
  * can boxplot for different categories
```R
> summary(tree$C)
 1  2  3  4 
 8 23 10 13 
# In other words, there are values 1, 2, 3, and 4, and they occur 8, 23, ... times each
> boxplot(tree$STBM~tree$C)
# Makes four boxplots of STBM separated according to their C value
```
 * scatter plot is just e.g. `plot(tree$STBM,tree$LFBM, main="Relationship Between Stem and Leaf Biomass", xlab="Stem Biomass", ylab="Leaf Biomass")`
 * `qqnorm(w1$vals)` then `qqline(w1$vals)` gives a qq plot to roughly check if values are not normally distributed

#### exporting and other stuff I googled

* plot saved to pdf
```R
> pdf("hist_w1.pdf") # can also add, e.g., width=6, height=3
> hist(w1$vals,breaks=10,main="Distribution of w1",xlab="w1")
> dev.off()
```
* multiplot
```R
> par(mfrow=c(2,2))
# Now can plot your four things, reads across row first
```
* adding bits to a single plot
```R
> hist(w1$vals,main='Leaf BioMass in High CO2 Environment',xlab='BioMass of Leaves',ylim=c(0,16))
> boxplot(w1$vals,horizontal=TRUE,at=16,add=TRUE,axes=FALSE)
> stripchart(w1$vals,add=TRUE,at=15)
# apparently this is a statistician's idea of a good time
```
 * or you could add points, e.g. `points(x1,y1,col=2,pch=2)`

Additional plotting here: http://www.cyclismo.org/tutorial/R/intermediatePlotting.html

## a few basic analyses

### least squares regression

```R
>  rate <- c(9.34 ,   8.50  ,  7.62  ,  6.93  ,  6.60)
>  year <- c(2000 ,   2001  ,  2002  ,  2003 ,   2004)
> cor(year,rate)
[1] -0.9880813
> fit <- lm(rate ~ year)
> fit

Call:
lm(formula = rate ~ year)

Coefficients:
(Intercept)         year  
   1419.208       -0.705  

> fit$coefficients[[1]] # Note use of double-square brackets to get number itself
[1] 1419.208
> 

# to plot
> plot(year,rate,
+      main="Commercial Banks Interest Rate for 4 Year Car Loan",
+      sub="http://www.federalreserve.gov/releases/g19/20050805/")
> abline(fit)

# test stats
> summary(fit)

Call:
lm(formula = rate ~ year)

Residuals:
     1      2      3      4      5 
 0.132 -0.003 -0.178 -0.163  0.212 

Coefficients:
              Estimate Std. Error t value Pr(>|t|)   
(Intercept) 1419.20800  126.94957   11.18  0.00153 **
year          -0.70500    0.06341  -11.12  0.00156 **

Residual standard error: 0.2005 on 3 degrees of freedom
Multiple R-squared:  0.9763,    Adjusted R-squared:  0.9684 
F-statistic: 123.6 on 1 and 3 DF,  p-value: 0.001559
```

### Confidence intervals

```R
> mean(w1$vals)
[1] 0.765
> error <- qt(0.975,df=length(w1$vals)-1)*sd(w1$vals)/sqrt(length(w1$vals))
> left <- mean(w1$vals)-error
> right <- mean(w1$vals)+error
> left
[1] 0.6617925
> right
[1] 0.8682075
# so there's a 95% probability that the true mean is between .66 and .87, assuming a normal distribution
```

## data management

* `v <- rbind(a,b)` will append rows of b onto rows of a
* `v <- cbind(a,b)` will append b as new columns onto end of a
* `names(v) <- c("col1", "col2", "col3", "col4")` to give them new names
* the above can also be used on matrices

### it does functional-ish programming (!)

* `lapply` applies a function to each element in a list
```R
> x <- list(a=rnorm(200,mean=1,sd=10), b=rexp(300,10.0), c=as.factor(c("a","b","b","b","c","c")))
> summary(x$a)
    Min.  1st Qu.   Median     Mean  3rd Qu.     Max. 
-35.8400  -6.0150   0.9325   0.8280   8.7310  35.8100
> lapply(x,summary)
$a
    Min.  1st Qu.   Median     Mean  3rd Qu.     Max. 
-35.8400  -6.0150   0.9325   0.8280   8.7310  35.8100 

$b
     Min.   1st Qu.    Median      Mean   3rd Qu.      Max. 
0.0003794 0.0325300 0.0749500 0.0971300 0.1318000 0.4934000 

$c
a b c 
1 3 2 
```
* `sapply` does what `lapply` does but will return the answer as a vector etc if possible and makes sense
```R
> xx <- list(a=rnorm(8,mean=1,sd=10),b=rexp(10,10.0))
> lapply(xx,mean)
$a
[1] 2.436018

$b
[1] 0.08651824

> sapply(xx,mean)
         a          b 
2.43601822 0.08651824 
```
* `tapply` applies the function to the first thing split up using the second as categories
```R
> heisenberg
  trial mass velocity
1     A 10.0       12
2     A 11.0       14
3     B  5.0        8
4     B  6.0       10
5     A 10.5       13
6     B  7.0       11
> tapply(heisenberg$mass, heisenberg$trial, mean)
   A    B 
10.5  6.0 
# more examples here: http://www.r-bloggers.com/r-function-of-the-day-tapply/

```

### (skipped time data type)

## scripts etc.

* use `source('simpleEx.R')` to run a script
* if statements
```R
if ( x < 0.2) {
    x <- x + 1
    cat("increment that number!\n")
} else if ( x < 2.0) {
    x <- 2.0*x
    cat("not big enough!\n")
} else {
    x <- x - 1
    cat("nah, make it smaller.\n");
}
```
* for loop is similar, uses `in` e.g. `for i in seq(0,1,by=0.3)`, nicer examples here: http://www.programiz.com/r-programming/for-loop
* `switch`, apparently it's faster than `if`
```R
> centre <- function(x, type) {
+ switch(type,
+        mean = mean(x),
+        median = median(x),
+        trimmed = mean(x, trim = .1))
+ }
> x <- rcauchy(10)
> centre(x, "mean")
[1] 0.8760325
> centre(x, "median")
[1] 0.5360891
> centre(x, "trimmed")
[1] 0.6086504
```

### functions

* return the last thing evaluated, or use `return(thing)` to specify what's returned
```R
> newDef <- function(a,b)
+  {
+      x = runif(10,a,b)
+      mean(x)
+  }
> newDef(-1,1)
[1] -0.2383129
> newDef(b=1,a=-1)
[1] -0.1982309
```
* if you go e.g. `source('newDef.R')` where it's defined, it becomes available to the workspace
* you can stick these in scripts etc. like you'd expect
* *functions will look outside themselves (e.g. in the workspace) for undefined variables!*
 * might be because the functions remember the environment that they were created in, they are closures, e.g.
```R
> f <- function(x) 0
> environment(f)
<environment: R_GlobalEnv>
# which is why it allows this kind of thing:
> y<-1
> f <- function(x){x+y}
> f(1)
[1] 2
# see http://www.quantide.com/R/ramarro-chapter-05/ for more
```

UP TO 16, object oriented programming - http://www.cyclismo.org/tutorial/R/objectOriented.html


# Ramarro's functional programming in R
http://www.quantide.com/R/ramarro-chapter-05/

## R is functional

R can do the 4 things of a functional programming language
1. passing functions as arguments to other functions
```R
> lapply(x,summary)
```
2. creating anonymous functions
```R
(function(x) sd(x)/mean(x))(x = 1:5)
[1] 0.5270463
```
3. returning functions as the values from other functions
```R
f <- function(){
  function(x) sd(x)/mean(x)
}
```
4. storing functions in data structures
```R
> f_list <- c(f,mean)
> f_list
[[1]]
function () 
{
    function(x) sd(x)/mean(x)
}

[[2]]
function (x, ...) 
UseMethod("mean")
<bytecode: 0x2cb6898>
<environment: namespace:base>
```

## function factory :-)

Making functions `f1, f2 ..., fi` that add `i` to the number given it
```R
> f <- function(i){
+   function(x) {x+i}
+ }
> f1 <- f(12)
> f12 <- f(12)
> f12(9)
[1] 21
```

# TODO -- the applys https://nsaunders.wordpress.com/2010/08/20/a-brief-introduction-to-apply-in-r/

