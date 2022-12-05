AOC 2022 - Day 3
================

## Part 1

``` r
assignments %>% 
 extract(packs, c("Elf1_start", "Elf1_end", "Elf2_start", "Elf2_end"), regex = "(\\d+)\\-(\\d+)\\,(\\d+)\\-(\\d+)") %>% 
 mutate(grp = 1:n(),
        Elf1_span = map2(Elf1_start,Elf1_end, ~.x:.y),
        Elf2_span = map2(Elf2_start,Elf2_end, ~.x:.y),
        overlap1 = map2_int(Elf1_span, Elf2_span, ~length(setdiff(.x,.y))),
        overlap2 = map2_int(Elf2_span, Elf1_span, ~length(setdiff(.x,.y)))) %>% 
 summarise(overlaps = sum(overlap1 == 0L | overlap2 == 0L))
```

    ## # A tibble: 1 × 1
    ##   overlaps
    ##      <int>
    ## 1      602

## Part 2

``` r
assignments %>% 
  extract(packs, c("Elf1_start", "Elf1_end", "Elf2_start", "Elf2_end"), regex = "(\\d+)\\-(\\d+)\\,(\\d+)\\-(\\d+)") %>% 
  mutate(grp = 1:n(),
         Elf1_span = map2(Elf1_start,Elf1_end, ~.x:.y),
         Elf2_span = map2(Elf2_start,Elf2_end, ~.x:.y),
         overlap1 = map2_int(Elf1_span, Elf2_span, ~length(intersect(.x,.y))),
         overlap2 = map2_int(Elf2_span, Elf1_span, ~length(intersect(.x,.y)))) %>% 
  summarise(overlaps = sum(overlap1 > 0L | overlap2 > 0L))
```

    ## # A tibble: 1 × 1
    ##   overlaps
    ##      <int>
    ## 1      891
