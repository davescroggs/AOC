AOC 2022 - Day 4
================

## Part 1

``` r
priority_df <- tibble(item = c(letters, LETTERS)) %>% 
                      mutate(priority = 1:n())

pack_items %>% 
  mutate(backpack = 1:n(),
         total_items = map_int(packs,str_length),
         c1 = str_sub(packs,end = total_items/2) %>% str_split(pattern = ""),
         c2 = str_sub(packs,start = total_items/2 + 1)%>% str_split(pattern = "")) %>% 
  mutate(common_item = map2_chr(c1, c2, ~intersect(.x, .y))) %>% 
  left_join(priority_df, by = c("common_item" = "item")) %>% 
  summarise(priority_sum = sum(priority))
```

    ## # A tibble: 1 × 1
    ##   priority_sum
    ##          <int>
    ## 1         8252

## Part 2

``` r
pack_items %>% 
  mutate(backpack = 1:n(),
         elves = rep(1:(n()/3), each = 3),
         total_items = map_int(packs,str_length)) %>% 
  group_by(elves) %>% 
  summarise(common_item = reduce(str_split(packs,pattern = ""),intersect)) %>% 
  left_join(priority_df, by = c("common_item" = "item")) %>% 
  summarise(priority_sum = sum(priority))
```

    ## # A tibble: 1 × 1
    ##   priority_sum
    ##          <int>
    ## 1         2828
