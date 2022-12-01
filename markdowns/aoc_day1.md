AOC 2022 - Day 1
================

## Part 1

### Test

The highest calorie holder has 24000 calories. Test the attempt until
the correct answer is returned.

``` r
### Create a function that reset the cumulative sum if the next value is NA/blank
rolling_sum_reset <- function(start, end){
    if(is.na(end)) return(0L) else return(start + end)
}
```

Run over the list pair-wise, using the accumulate function and record
the result after each pair of cells

``` r
## Accumulate result of function call and find max
purrr::accumulate(test_data,rolling_sum_reset) |> max()
```

    ## [1] 24000

### Solution

``` r
cumulative_cals <- purrr::accumulate(calories,rolling_sum_reset) 
max(cumulative_cals)
```

    ## [1] 69206

# Part 2

Find top 3 calorie carriers and sum them

``` r
# Solution part 2
sort(cumulative_cals, decreasing = T)[1:3] |> sum()
```

    ## [1] 197400
