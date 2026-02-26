Functions
================

# **What is a Function?**

A function is a reusable block of code that accepts input arguments and
produces output by executing a set of code statements. Functions can be
provided by R or packages or user defined (created by you).

Ready made Functions

R comes with many pre built functions for common tasks. Some examples
include:

- unique() - returns the unique values from a vector or data frame
  column
- summary() - provides descriptive statistics for a data frame or vector
- length() - returns the number of elements in a vector
- mean(), median(), sd() - calculate descriptive statistics

**Why Create User Defined Functions?**

User-defined functions offer several important advantages:

- Code reusability: Write the code once and call it multiple times,
  reducing redundancy.
- Optimization: Consolidate repeated code into a single, efficient
  block.
- Error reduction: Minimize copy paste errors and inconsistencies in
  your code.
- Readability: Make your code more organized and easier to understand.
- Maintainability: Update code/information in one place rather than
  multiple locations.

**Creating a function in R**

To make a function this format needs to be used.

``` r
function_name_ <- function(parameters){body}


function_name # The function name is the identifier you use to call your function. When you define a function, it is stored as an object in your R environment. Choose names that are concise, clear, and meaningful to describe what the function does.

function(parameters) # Parameters (also called formal arguments) are variables defined in the function definition that represent inputs the function will receive. Parameters are enclosed in parentheses and separated by commas. For example
 
  circumference <- function(r){
    2*pi*r}
  print(circumference(2))
  
{body} # The function body contains the code statements that execute when the function is called. This is where you perform calculations, manipulations, or other operations on the input parameters. The function body is enclosed in curly braces {}.
```

Return Values = Functions typically return output using the return()
statement. This specifies what result the function produces. If no
explicit return() statement is included, R returns the value of the last
expression evaluated in the function.

Calling a Function = Once defined, you call a function by using its name
followed by parentheses containing the argument values:
calculate_average(5, 10) \# Returns 7.5

## **Example**

``` r
calculate_calories_women <- function(weight, height, age){
    (10 * weight) + (6.25 * height) - (5 * age) - 161}
```

- This calculates the basal metabolic rate.
- For women the formula is (10 x weight) + (6.25 x height) - (5 x age) -
  161
- To calculate the daily consumption of calories for a women who is 30,k
  weights 60kg and is 165cm tall

``` r
print(calculate_calories_women(60, 165, 30))
```

    ## [1] 1320.25

# **Function Creation**

## 1st itiration

``` r
fast_plot1 <- function(v, col_name){
  ggplot(data.frame(x = factor(v), Sex = df$Gender), aes(x = x, fill = Sex)) +
    geom_bar(position = "dodge") + 
    theme_light() + 
    theme(axis.text.x = element_text(angle = 90)) +
    labs(x = col_name)
}
fast_plot1(df$Ethnicity_UK_recode, "Ethnicity_UK_recode")
```

![](Functions_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

``` r
fast_plot = name of the function

function_ =function code

(v) = place holder for variable (like x in algebra)

col_name) = It is a placeholder for information to pass on into the function. In this case _col_name_ stores the name of the column displayed as the x-axis label.

{ = Opens the function body 

ggplot() = starts the plot

data.frame(x = factor(V, Gender = df$Gender) = creates a data frame with two columns
  + x = the variable pulled in from original data set (converted to categories with factor())
  + Gender = the Gender column from the data set
  
aes(x=x, fill = Gender) = sets up the aesthetics
  + x=x - puts variable on the x axis
  + fill = Gender = colours the bars by Gender
  
geom_bar(position = "dodge") = creates bar chart and places bars side-by-side

theme_light() = applies light theme

theme(axis.text.x = element_text(angle = 90)) = Rotates x axis labels to 90 degrees

labs(x = col_name) = adds label to plot
```

## as.character

To make sure all the values have been pulled from the data set you need
to include **as.character**.

You need to change from factor(v) to factor(as.character(v)) at the
beginning of the code.

This ensures all the values are extracted from the data set.

``` r
fast_plot1 <- function(v, col_name){
  ggplot(data.frame(x = factor(as.character(v)), Sex = df$Sex), aes(x = x, fill = Sex)) +
    geom_bar(position = "dodge") + 
    theme_light() + 
    theme(axis.text.x = element_text(angle = 90)) +
    labs(x = col_name)
}

fast_plot1(df$Ethnicity_UK_recode, "Ethnicity_UK_recode")
```

![](Functions_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

## Converting the NAs’

Sometimes in a data set there will be NAs which have been manually put
in and naturally occurring NAs which appear when the cell was left
blank. To include all these values into the graph you need to add this
code. Furthermore, this shows how to change values into different
meaning which can be useful.

Adding the v\[is.na(v)\] \<- “NA”\_ and v\[v == “NA”\] \<- “NA” confirms
the NA values will be shown as they should be.

``` r
fast_plot1 <- function(v, col_name){
  v[is.na(v)] <- "NA"
  v[v == "NA"] <- "NA"
  
  ggplot(data.frame(x = factor(as.character(v)), Sex = df$Sex), aes(x = x, fill = Sex)) +
    geom_bar(position = "dodge") + 
    theme_light() + 
    theme(axis.text.x = element_text(angle = 90)) +
    labs(x = col_name)
}

fast_plot1(df$Ethnicity_UK_recode, "Ethnicity_UK_recode")
```

![](Functions_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

## Numeric Values

Data sets can include values which are numeric like age or weight. These
need to be converted to as.numeric after they have been pulled from the
data set using as.character. This means when they are plotted R
recognizes them as numbers instead of text.

Here is the coding;

- as.character - to pull all the data from the data set
- v\[is.na(v)\] \<- “-9” v\[v == “NA”\] \<- “-9” = to convert the values
  to “-9”
- as.numeric = to change the format of the data into its numeric format
  for plotting

``` r
fast_plot_numeric <- function(v, col_name){
  v <- as.character(v)
  v[is.na(v)] <- "-9"
  v[v == "NA"] <- "-9"
  v <- as.numeric(v)
  
  ggplot(data.frame(x = v, Sex = df$Sex), aes(x = v, fill = Sex)) +
    geom_bar(position = "dodge") + 
    theme_light() + 
    theme(axis.text.x = element_text(angle = 90, hjust = 0.5)) +
    labs(x = col_name)
}

fast_plot_numeric(df$AgeAtAssessment, "AgeAtAssessment")
```

![](Functions_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

## Adding assertions

Assertions in R, is a statement which checks whether a condition is
true, if it is false, the execution stops and returns an error code. The
code for this is

``` r
stopifnot()
```

``` r
fast_plot_numeric <- function(v, col_name){
  # Check that v is numeric
  stopifnot(is.character(v))
  
  v <- as.character(v)
  v[is.na(v)] <- "NA"
  v[v == "NA"] <- "NA"
  v <- as.character(v)
  
  ggplot(data.frame(x = v, Sex = df$Sex), aes(x = v, fill = Sex)) +
    geom_bar(position = "dodge") + 
    theme_light() + 
    theme(axis.text.x = element_text(angle = 90, hjust = 0.5)) +
    labs(x = col_name)
}
fast_plot_numeric(df3, "df3")
fast_plot_numeric(df$Ethnicity_UK_recode, "Ethnicity_UK_recode")
```

## Known encoding

This code can be used for example when you know the encoding of the
variable and you need it to be converted for plotting.

``` r
fast_plot_known_encoding <- function(v, col_name){
  v <- as.character(v)
  v[is.na(v)] <- "NA"
  v[v == "NA"] <- "NA"
  v[v == "0"] <- "No"
  v[v == "1"] <- "Yes"
  
  ggplot(data.frame(x = v, Sex = df$Sex), aes(x = v, fill = Sex)) +
    geom_bar(position = "dodge") + 
    theme_light() + 
    theme(axis.text.x = element_text(angle = 90, hjust = 0.5)) +
    labs(x = col_name)
}

fast_plot_known_encoding(df$Asthma, "Asthma")
```

![](Functions_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->

## Histogram

This changes the bar graphs to histograms used for decimals.

``` r
df3 <- c(52.3, 55.8, 58.2, 61.5, 64.1, 66.8, 69.2, 71.5, 73.8, 76.2, 78.5, 80.9, 83.2, 85.6, 87.9, 90.2, 92.5, 94.8, 97.1, 99.4, 54.2, 57.1, 60.3, 63.4, 66.5, 69.7, 72.8, 75.9, 79.1, 82.2, 85.3, 88.5, 91.6, 94.7, 97.9, 52.8, 56.4, 59.7, 62.9, 66.1, 69.3, 72.5, 75.7, 78.9, 82.1, 85.3, 88.5, 91.7, 94.9, 98.1, 53.5, 56.9, 60.1, 63.2, 66.3, 69.4, 72.5, 75.6, 78.7, 81.8, 84.9, 88.0, 91.1, 94.2, 97.3, 54.7, 57.8, 60.9, 64.0, 67.1, 70.2, 73.3, 76.4, 79.5, 82.6, 85.7, 88.8, 91.9, 95.0, 98.1, 55.3, 58.5, 61.7, 64.9, 68.1, 71.3, 74.5, 77.7, 80.9, 84.1, 87.3, 90.5, 93.7, 96.9, 60.2, 65.4, 70.6, 75.8, 81.0, 86.2, 91.4, 96.6)

fast_plot_histogram <- function(v, col_name){
  v <- as.character(v)
  v[is.na(v)] <- "-9"
  v[v == "NA"] <- "-9"
  v <- as.numeric(v)
  
  ggplot(data.frame(x = v), aes(x = v)) +
    geom_histogram(position = "dodge", bins = 200, color = "white", fill = "tomato") + 
    theme_light() + 
    theme(axis.text.x = element_text(angle = 0, hjust = 0.5)) +
    labs(x = col_name)
}

fast_plot_histogram(df3, "df3")
```

![](Functions_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

``` r
fast_plot_histogram_real_example <- function(v, col_name){
  v <- as.character(v)
  v[is.na(v)] <- "-9"
  v[v == "NA"] <- "-9"
  v <- as.numeric(v)
  
  ggplot(data.frame(x = v, Gender = df$Gender), aes(x = v, fill = Gender)) +
    geom_histogram(position = "dodge") + 
    theme_light() + 
    theme(axis.text.x = element_text(angle = 0, hjust = 0.5)) +
    labs(x = col_name)
}

fast_plot_histogram_real_example(df$clozapine_exposure_months, "clozapine_exposure_months")
```

    ## `stat_bin()` using `bins = 30`. Pick better value `binwidth`.

![](Functions_files/figure-gfm/unnamed-chunk-14-1.png)<!-- -->

## Regession line example

``` r
# Create a dataset
set.seed(42)  # for reproducibility, this pulls Rs random number generator. Without this rnorm() generates different random values every time you run the script. With set.seed you get the same data set each time.

n <- 100 # number of values

height <- rnorm(n, mean = 170, sd = 10)  # This generates 100 random height values that follow a normal (bell-curve) distribution. The mean = 170 means the average height is 170 cm, and sd = 10 means most values cluster within 10 cm of that average. So you'd get heights ranging roughly between 150-190 cm, centered around 170.

weight <- 0.5 * height + rnorm(n, mean = -35, sd = 15)  # This creates weight values with a deliberate relationship to height. This is because the height is multiplied by 0.5. Next subtracts 35 on average, plus adds some random noise. The rnorm(n, mean = -35, sd = 15) adds the noise which makes the data more realistic.

# Combine into a data frame
data <- data.frame(height = height, weight = weight)
```

``` r
regression_function <- function(w, h) {
  regression_model <- lm(h ~ w) # This makes the regression model, height vs "~" weight.
  print(summary(regression_model)) # This should print the useful information about the regression line.
  plot(w, h, main = "Height vs Weight", xlab = "Height (cm)", ylab = "Weight (kg)") # main = adds a title
  abline(regression_model, col = "seagreen") # Adds regression line
}
```

``` r
regression_function(data$weight, data$height)
```

    ## 
    ## Call:
    ## lm(formula = h ~ w)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -34.617  -6.909  -0.123   6.647  18.676 
    ## 
    ## Coefficients:
    ##              Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept) 157.03095    3.37430  46.537  < 2e-16 ***
    ## w             0.27214    0.06618   4.112 8.16e-05 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 9.666 on 98 degrees of freedom
    ## Multiple R-squared:  0.1472, Adjusted R-squared:  0.1385 
    ## F-statistic: 16.91 on 1 and 98 DF,  p-value: 8.158e-05

![](Functions_files/figure-gfm/unnamed-chunk-17-1.png)<!-- -->

## NCMH examples

``` r
fast_plot1(df$Ethnicity_UK_recode, "Ethnicity_UK_recode")
```

![](Functions_files/figure-gfm/unnamed-chunk-18-1.png)<!-- -->

``` r
fast_plot_numeric(df$ChildrenNumber, "ChildrenNumber")
```

![](Functions_files/figure-gfm/unnamed-chunk-18-2.png)<!-- -->

``` r
fast_plot_known_encoding(df$Autism, "Autism")
```

![](Functions_files/figure-gfm/unnamed-chunk-18-3.png)<!-- -->

``` r
fast_plot_histogram_real_example(df$lithium_exposure_months, "Lithium_exposure_months")
```

    ## `stat_bin()` using `bins = 30`. Pick better value `binwidth`.

![](Functions_files/figure-gfm/unnamed-chunk-18-4.png)<!-- -->

# **Using the if/else code**

The next step is to write one function which checks whether the input is
numeric or a character to then choose the appropriate plotting pathway.

## Step 1

To determine if a variable contains numeric values, you can use
`is.numeric()`. However, this function only checks the data type, not
whether text-based data looks numeric (like “123” stored as text).

Instead `suppressWarnings(as.numeric(v))` is used. This attempts to
convert the values to numeric format. If the conversion succeeds (even
if some values become NA), the data is numeric-like. The
`suppressWarnings()` part suppresses conversion warning messages that
would otherwise appear when non-numeric text cannot be converted.

This pattern works because: - Text that looks numeric (like “42” or
“3.14”) will convert successfully - Non-numeric text (like “Male” or
“Unknown”) will become NA without stopping the function -
`suppressWarnings()` keeps your output clean by hiding the expected
conversion warnings

``` r
is_num <- suppressWarnings(is.numeric(as.numeric(v)))
```

## Step 2.a

The next step is using the *if/else* code. This is how R makes
decisions. It means;

- IF something is true \<- do this
- ELSE \<- fo something different.

**The condition must be TRUE or FALSE**

For this you need to use the curly brackets.

- if = the R if
- (condition) = what you would like the “if” to be
- open curly brackets to show the code if it is the “if”

For example

``` r
if (condition) {
  # code that runs if condition is TRUE
} else {
  # code that runs if condition is FALSE
}
```

## Step 2.b

Inside the function *if* decides which code the function runs.

The function returns whatever block is chosen.

The other block is completely ignored.

Example

``` r
describe_number <- function(x) {
  if (x > 0) {
    "positive"
  } else {
    "zero or negative"
  }
}
```

``` r
describe_number(5)
```

    ## [1] "positive"

``` r
# "positive"

describe_number(-2)
```

    ## [1] "zero or negative"

``` r
# "zero or negative"
```

## Example

``` r
do_you_like_R <- function(x) {
  if (x == "yes") {
    "yippee R is amazing"
  } else {
    "not yet :("
  }
}
```

``` r
do_you_like_R("yes")
```

    ## [1] "yippee R is amazing"

``` r
do_you_like_R("no")
```

    ## [1] "not yet :("

## Text and numeric example

``` r
fast_plot2 <- function(v, col_name) { # This is naming the function. v is the input.
  
  # Test if values are numeric-like
  numeric_test <- suppressWarnings(as.numeric(v)) # This tries to convert all the values in "v" to numbers. If a value cannot be converted because it is text it is converted to "NA". Supress warnings hides any warning messages from the conversion.
  is_num <- !all(is.na(numeric_test)) # This checks is every value in numeric_test is NA. Returns TRUE if all values are NA (meaning nothing was converted to numeric). Returns FALSE if at least some of the values have been converted to numeric.
  
  # The "!" flips this result so is.num is TRUE if the data is numeric like and FALSE if there is text.
  
  if (is_num) { # Checks if the data is numeric, if TRUE, this code block is executed
    
    # ----- NUMERIC CASE -----
    
    v <- suppressWarnings(as.numeric(v)) # Converts all the values in v to numeric format
    v[is.na(v)] <- -9 # Converts the NAs into -9.
    
    ggplot( # creates a ggplot
      data.frame(x = v), # Puts the numeric values into a data frame with the column name "x"
      aes(x = x) #shows the "x" column on the x-axis.
    ) +
      geom_bar(position = "dodge", fill = "orange2") + # makes a bar graph, where the bars are placed side by side and coloured "orange2"
      theme_light() + # Uses the light theme
      labs(x = col_name) # Labels the x-axis label the column name
      
  } else { # Everything in these {} brackets will run when the data fails the numeric test. 
    # ----- TEXT CASE -----
    v <- as.character(v)
    v[is.na(v)] <- "NA"
    v[v == "0"] <- "No"
    v[v == "1"] <- "Yes"
    
    ggplot(data.frame(x = v), aes(x = v)) +
      geom_bar(position = "dodge", fill = "orchid") + 
      theme_light() + 
      theme(axis.text.x = element_text(angle = 90, hjust = 0.5)) +
      labs(x = col_name)
  }
}
```

``` r
fast_plot2(df2$text, "text")
```

![](Functions_files/figure-gfm/unnamed-chunk-26-1.png)<!-- -->

``` r
fast_plot2(df2$numbers, "numbers")
```

![](Functions_files/figure-gfm/unnamed-chunk-26-2.png)<!-- -->

## Text, numeric and histogram example

When you have more than one possible outcome you need to use and “if”
inside of an “if”. This is called an “nested if statement”.

In this example the first if shows if the data is numeric or text. If
the numbers contain decimals then a histogram is plotted, if the numbers
are integers then a bar chart is plotted. However if there is text the
variables skips the nested if and goes straight tot he text plotting.

``` r
fast_plot3 <- function(v, col_name) {
  
  # Test if values are numeric-like
  numeric_test <- suppressWarnings(as.numeric(v))
  is_num <- !all(is.na(numeric_test))
  
  if (is_num) {
    # ----- NUMERIC CASE -----
    v <- suppressWarnings(as.numeric(v))
    v[is.na(v)] <- -9
    
    # Check if values contain decimals
    is_decimal <- any(v %% 1 != 0, na.rm = TRUE) # v %% 1 = The modulo operator which returns the remainder after division. e.g. 
                                                    # For 2.5 %% 1 = 0.5 (remainder after dividing by 1)
                                                 # ! = 0 = Checks if the remainder is NOT equal to zero e.g.
                                                    # 0.5 != 0 -> TRUE (has no decimal)
                                                    # 0 != 0 -> FALSE (no decimal, 0 is a whole number)
                                                 # na.rm = TRUE = Ignores NA values when checking
    
    
    if (is_decimal) {
      # ----- DECIMAL/CONTINUOUS CASE -----
      ggplot(
        data.frame(x = v),
        aes(x = x)
      ) +
        geom_histogram(bins = 30, fill = "seagreen4") +
        theme_light() +
        labs(x = col_name, y = "Frequency")
        
    } else {
      # ----- INTEGER CASE -----
      ggplot(
        data.frame(x = v),
        aes(x = x)
      ) +
        geom_bar(position = "dodge", fill = "orange2") +
        theme_light() +
        labs(x = col_name)
    }
      
  } else {
    # ----- TEXT CASE -----
    v <- as.character(v)
    v[is.na(v)] <- "NA"
    v[v == "0"] <- "No"
    v[v == "1"] <- "Yes"
    
    ggplot(data.frame(x = v), aes(x = v)) +
      geom_bar(position = "dodge", fill = "orchid") + 
      theme_light() + 
      theme(axis.text.x = element_text(angle = 90, hjust = 0.5)) +
      labs(x = col_name)
  }
}
```

``` r
fast_plot3(df2$text, "text")
```

![](Functions_files/figure-gfm/unnamed-chunk-28-1.png)<!-- -->

``` r
fast_plot3(df2$numbers, "numbers")
```

![](Functions_files/figure-gfm/unnamed-chunk-28-2.png)<!-- -->

``` r
fast_plot3(df2$decimals, "decimals")
```

![](Functions_files/figure-gfm/unnamed-chunk-28-3.png)<!-- -->

## NCMH examples

``` r
fast_plot3(df$Ethnicity_UK_recode, "Ethnicity_UK_recode")
```

![](Functions_files/figure-gfm/unnamed-chunk-29-1.png)<!-- -->

``` r
fast_plot3(df$ChildrenNumber, "ChildrenNumber")
```

![](Functions_files/figure-gfm/unnamed-chunk-29-2.png)<!-- -->
