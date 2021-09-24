Homework1
================

\#Problem 1 \# Setup

I will start by loading the tidyverse.

``` r
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.1 ──

    ## ✓ ggplot2 3.3.5     ✓ purrr   0.3.4
    ## ✓ tibble  3.1.4     ✓ dplyr   1.0.7
    ## ✓ tidyr   1.1.3     ✓ stringr 1.4.0
    ## ✓ readr   2.0.1     ✓ forcats 0.5.1

    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

\#Variable Initialization

``` r
#First I am going to initialize the vectors

#Here I initialize a random sample of size 10 from a standard Normal distribution
sample <- rnorm(10)
#Here I initialize a logical vector indicating whether elements of the sample are greater than 0
logical_vector <- sample > 0
#Here I initialize a character vector of length 10
character_vector <- c("a","b","c","d","e","f","g","h","i","j")
#Here I initialize a factor vector of length 10, with 3 different factor “levels”
factor_vector <- factor(c(1,1,1,2,2,2,3,3,3,1))
```

\#Vector Characterization

``` r
#Now I am going to characterize the vectors
#Here I check the length of the sample vector
length(sample) 
```

    ## [1] 10

``` r
#Here I check the length of the logical vector
length(logical_vector) 
```

    ## [1] 10

``` r
#Here I check the length of the character vector
length(character_vector) 
```

    ## [1] 10

``` r
#Here I check the length of the factor vector
length(factor_vector) 
```

    ## [1] 10

``` r
#Here I check the levels of the factor vector
levels(factor_vector) 
```

    ## [1] "1" "2" "3"

\#Dataframe Initialization

``` r
#Now I am going to make the dataframe
homework_one_df <- tibble(
  sample, logical_vector, character_vector, factor_vector
)
```

\#Calculating vector means

``` r
#Now I am going to calculate the means of each vector
#Here I check the mean of the sample vector
mean (sample) 
```

    ## [1] 0.212684

``` r
#Here I check the mean of the logical vector
mean(logical_vector) 
```

    ## [1] 0.5

``` r
#Here I check the mean of the character vector
mean(character_vector) 
```

    ## Warning in mean.default(character_vector): argument is not numeric or logical:
    ## returning NA

    ## [1] NA

``` r
#Here I check the mean of the factor vector
mean(factor_vector)
```

    ## Warning in mean.default(factor_vector): argument is not numeric or logical:
    ## returning NA

    ## [1] NA

``` r
#The sample and logical vectors returned means, but the character and factor vectors did not.
```

\#Using the pull function

``` r
#I can also take the means of the vectors by extracting them from the dataframe with the pull function
#A pipeline to check the mean of the sample
homework_one_df %>% pull (sample) %>% mean() 
```

    ## [1] 0.212684

``` r
#A pipeline to check the mean of the logical vector
homework_one_df %>% pull (logical_vector) %>% mean() 
```

    ## [1] 0.5

``` r
#A pipeline to check the mean of the character vector
homework_one_df %>% pull (character_vector) %>% mean()
```

    ## Warning in mean.default(.): argument is not numeric or logical: returning NA

    ## [1] NA

``` r
#A pipeline to check the mean of the factor vector
homework_one_df %>% pull (factor_vector) %>% mean() 
```

    ## Warning in mean.default(.): argument is not numeric or logical: returning NA

    ## [1] NA

\#Problem 2 The “palmerpenguins” package was installed

``` r
#Here I load the penguins data set
data("penguins", package = "palmerpenguins")
#I will inspect the structure of the penguins data set
str(penguins)
```

    ## tibble [344 × 8] (S3: tbl_df/tbl/data.frame)
    ##  $ species          : Factor w/ 3 levels "Adelie","Chinstrap",..: 1 1 1 1 1 1 1 1 1 1 ...
    ##  $ island           : Factor w/ 3 levels "Biscoe","Dream",..: 3 3 3 3 3 3 3 3 3 3 ...
    ##  $ bill_length_mm   : num [1:344] 39.1 39.5 40.3 NA 36.7 39.3 38.9 39.2 34.1 42 ...
    ##  $ bill_depth_mm    : num [1:344] 18.7 17.4 18 NA 19.3 20.6 17.8 19.6 18.1 20.2 ...
    ##  $ flipper_length_mm: int [1:344] 181 186 195 NA 193 190 181 195 193 190 ...
    ##  $ body_mass_g      : int [1:344] 3750 3800 3250 NA 3450 3650 3625 4675 3475 4250 ...
    ##  $ sex              : Factor w/ 2 levels "female","male": 2 1 1 NA 1 2 1 2 NA NA ...
    ##  $ year             : int [1:344] 2007 2007 2007 2007 2007 2007 2007 2007 2007 2007 ...

``` r
#There are 8 variables of the penguins data set include species (factor vector with 3 levels), island (factor vector with 3 levels), bill length (mm), bill depth (mm), flipper length (mm), body mass (g), sex and year. 
#Species and island are factor vectors with 3 levels, bill length and depth are numeric vectors, flipper length and body mass are integer vectors, sex is a factor vector with 2 levels, and year is an integer vector.
#From the output of structure we know that the data set has 344 rows and 8 columns.
#I will verify the dimensions of the penguins data structure with nrow and ncol functions.
nrow(penguins)
```

    ## [1] 344

``` r
ncol(penguins)
```

    ## [1] 8

``` r
#These outputs verify the dimensions of the penguins are 344 x 8
#Here I will calculate the mean flipper length
penguins %>% pull (flipper_length_mm) %>% mean()
```

    ## [1] NA

``` r
#Since the output was "NA" I will inspect the data for that column
penguins %>% pull (flipper_length_mm)
```

    ##   [1] 181 186 195  NA 193 190 181 195 193 190 186 180 182 191 198 185 195 197
    ##  [19] 184 194 174 180 189 185 180 187 183 187 172 180 178 178 188 184 195 196
    ##  [37] 190 180 181 184 182 195 186 196 185 190 182 179 190 191 186 188 190 200
    ##  [55] 187 191 186 193 181 194 185 195 185 192 184 192 195 188 190 198 190 190
    ##  [73] 196 197 190 195 191 184 187 195 189 196 187 193 191 194 190 189 189 190
    ##  [91] 202 205 185 186 187 208 190 196 178 192 192 203 183 190 193 184 199 190
    ## [109] 181 197 198 191 193 197 191 196 188 199 189 189 187 198 176 202 186 199
    ## [127] 191 195 191 210 190 197 193 199 187 190 191 200 185 193 193 187 188 190
    ## [145] 192 185 190 184 195 193 187 201 211 230 210 218 215 210 211 219 209 215
    ## [163] 214 216 214 213 210 217 210 221 209 222 218 215 213 215 215 215 216 215
    ## [181] 210 220 222 209 207 230 220 220 213 219 208 208 208 225 210 216 222 217
    ## [199] 210 225 213 215 210 220 210 225 217 220 208 220 208 224 208 221 214 231
    ## [217] 219 230 214 229 220 223 216 221 221 217 216 230 209 220 215 223 212 221
    ## [235] 212 224 212 228 218 218 212 230 218 228 212 224 214 226 216 222 203 225
    ## [253] 219 228 215 228 216 215 210 219 208 209 216 229 213 230 217 230 217 222
    ## [271] 214  NA 215 222 212 213 192 196 193 188 197 198 178 197 195 198 193 194
    ## [289] 185 201 190 201 197 181 190 195 181 191 187 193 195 197 200 200 191 205
    ## [307] 187 201 187 203 195 199 195 210 192 205 210 187 196 196 196 201 190 212
    ## [325] 187 198 199 201 193 203 187 197 191 203 202 194 206 189 195 207 202 193
    ## [343] 210 198

``` r
#I will remove the "NA" values from the data frame, which makes the mean function unable to calculate a numeric output. Then, I will calculate the mean of the remaining values in the flipper length column.
penguins %>% drop_na() %>% pull(flipper_length_mm) %>% mean()
```

    ## [1] 200.967

``` r
##The mean flipper length is 200.967 mm.
```
