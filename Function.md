STAT 545B Assignment 1
================
Xuan Li
2024/10/29

## Introduction

This rmd file includes creating, documenting, and testing a custom R
function called `scale_and_multiply`. The function takes a numeric
vector, scales it between 0 and 1, and then multiplies it by a specified
value. The assignment is separated into 4 exerices.

## Exercise 1: Creating the Function

In this exerice, we create the function.

``` r
scale_and_multiply <- function(x, multiplier) {
  # Ensure both inputs are numeric
  stopifnot(is.numeric(x), is.numeric(multiplier))
  
  # Scale the vector to a 0-1 range
  scaled_x <- (x - min(x, na.rm = TRUE)) / (max(x, na.rm = TRUE) - min(x, na.rm = TRUE))
  
  # Multiply the scaled vector by the multiplier
  result <- scaled_x * multiplier
  return(result)
}
```

## Exercise 2: Creating Documentation

In this exercise, we document the function.

``` r
#' The function name is: Scale and Multiply
#' This function scales a numeric vector to the range [0, 1] and then multiplies each element by a specified multiplier.
#' It can be called by: scale_and_multiply(x, multiplier)
#'
#' @param x A numeric vector to be scaled and multiplied, we name it x, representing input values like f(x) = y
#' @param multiplier A numeric value by which to multiply the scaled vector, we name it directly as multiplier
#' @return A numeric vector with scaled and multiplied values.
#' @examples
#' scale_and_multiply(c(1, 2, 3, 4), 10)
#' scale_and_multiply(c(10, 20, 30), 0.5)
scale_and_multiply <- function(x, multiplier) {
  stopifnot(is.numeric(x), is.numeric(multiplier))
  scaled_x <- (x - min(x, na.rm = TRUE)) / (max(x, na.rm = TRUE) - min(x, na.rm = TRUE))
  result <- scaled_x * multiplier
  return(result)
}
```

## Exercise 3: Creating Examples

in this exercise, we create exmaples for the function we built.

``` r
# Example 1: Standard scaling and multiplying
scale_and_multiply(c(1, 2, 3, 4), 10)
```

    ## [1]  0.000000  3.333333  6.666667 10.000000

``` r
# Example 2: Scaling a larger range and multiplying by a fraction
scale_and_multiply(c(10, 20, 30), 0.5)
```

    ## [1] 0.00 0.25 0.50

``` r
# Example 3: Testing with a more varied range, including negative values
scale_and_multiply(c(-5, 0, 5, 10), 3)
```

    ## [1] 0 1 2 3

## Exercise 4: Creating Tests

In this exercise, we create tests using testthat on our function.

``` r
library(testthat)

test_that("Testing scale_and_multiply function", {
  # Test with standard numeric input
  expect_equal(scale_and_multiply(c(1, 0, 0.2, 0.8), 1), c(1, 0, 0.2, 0.8), tolerance = 1e-4)
  
  # Test with a vector containing negative values
  expect_equal(scale_and_multiply(c(-5, 0, 5), 2), c(0, 1, 2), tolerance = 1e-4)
  
  # Test that a non-numeric input throws an error
  expect_error(scale_and_multiply("hello", 5))
  
  # Test that a non-numeric multiplier throws an error
  expect_error(scale_and_multiply(c(1, 2, 3), "5"))
})
```

    ## Test passed 😀
