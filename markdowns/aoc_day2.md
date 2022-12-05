AOC 2022 - Day 2
================

## Part 1

``` r
tbl %>% 
  extract(col = moves, into = c("Opponent", "Me"), regex = "(.) (.)") %>% 
  left_join(guide, by = c("Opponent" = "moves")) %>% 
  left_join(points_df, by = "Me") %>% 
  mutate(outcome = case_when(
    Me == winning_move ~ 6L,
    Me == losing_move ~ 0L,
    TRUE ~ 3L)) %>% 
  summarise(final_score = sum(points + outcome))
```

    ## # A tibble: 1 × 1
    ##   final_score
    ##         <int>
    ## 1       12458

Attempt 1 - 9275 (too low)

Attempt 3 - 13122 (too high)

Attempt 4 - 12458 (correct)

## Part 2

``` r
guide_part2 <- tibble(Me = c("X", "Y", "Z"),
                      result = c("L", "D", "W"))

tbl %>% 
  extract(col = moves, into = c("Opponent", "Me"), regex = "(.) (.)") %>% 
  left_join(guide, by = c("Opponent" = "moves")) %>% 
  left_join(guide_part2, by = "Me") %>% 
  mutate(my_move = case_when(
    result == "W" ~ winning_move,
    result == "L" ~ losing_move,
    result == "D" ~ drawing_move),
    outcome = case_when(
    result == "W" ~ 6L,
    result == "L" ~ 0L,
    result == "D" ~ 3L)) %>% 
  left_join(points_df, by = c("my_move" = "Me")) %>% 
   summarise(final_score = sum(points + outcome))
```

    ## # A tibble: 1 × 1
    ##   final_score
    ##         <int>
    ## 1       12683
