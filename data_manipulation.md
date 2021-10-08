Data Manipulation Lecture
================

## Import some data

Importing `FAS_litters.csv` and clean up the variable names.

``` r
litters_df = read_csv("data/FAS_litters.csv")
```

    ## Rows: 49 Columns: 8

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr (2): Group, Litter Number
    ## dbl (6): GD0 weight, GD18 weight, GD of Birth, Pups born alive, Pups dead @ ...

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
litters_df = janitor::clean_names(litters_df)

pups_df = read_csv("data/FAS_pups.csv")
```

    ## Rows: 313 Columns: 6

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr (1): Litter Number
    ## dbl (5): Sex, PD ears, PD eyes, PD pivot, PD walk

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
pups_df = janitor::clean_names(pups_df)
```

## `select` function

Select only the columns you’re interested in.

``` r
select(litters_df, group, litter_number) # selects these variables
```

    ## # A tibble: 49 x 2
    ##    group litter_number  
    ##    <chr> <chr>          
    ##  1 Con7  #85            
    ##  2 Con7  #1/2/95/2      
    ##  3 Con7  #5/5/3/83/3-3  
    ##  4 Con7  #5/4/2/95/2    
    ##  5 Con7  #4/2/95/3-3    
    ##  6 Con7  #2/2/95/3-2    
    ##  7 Con7  #1/5/3/83/3-3/2
    ##  8 Con8  #3/83/3-3      
    ##  9 Con8  #2/95/3        
    ## 10 Con8  #3/5/2/2/95    
    ## # ... with 39 more rows

``` r
select(litters_df, group, gd0_weight, gd18_weight) 
```

    ## # A tibble: 49 x 3
    ##    group gd0_weight gd18_weight
    ##    <chr>      <dbl>       <dbl>
    ##  1 Con7        19.7        34.7
    ##  2 Con7        27          42  
    ##  3 Con7        26          41.4
    ##  4 Con7        28.5        44.1
    ##  5 Con7        NA          NA  
    ##  6 Con7        NA          NA  
    ##  7 Con7        NA          NA  
    ##  8 Con8        NA          NA  
    ##  9 Con8        NA          NA  
    ## 10 Con8        28.5        NA  
    ## # ... with 39 more rows

``` r
select(litters_df, group, gd0_weight:gd_of_birth) # selects everything in range
```

    ## # A tibble: 49 x 4
    ##    group gd0_weight gd18_weight gd_of_birth
    ##    <chr>      <dbl>       <dbl>       <dbl>
    ##  1 Con7        19.7        34.7          20
    ##  2 Con7        27          42            19
    ##  3 Con7        26          41.4          19
    ##  4 Con7        28.5        44.1          19
    ##  5 Con7        NA          NA            20
    ##  6 Con7        NA          NA            20
    ##  7 Con7        NA          NA            20
    ##  8 Con8        NA          NA            20
    ##  9 Con8        NA          NA            20
    ## 10 Con8        28.5        NA            20
    ## # ... with 39 more rows

``` r
select(litters_df, -litter_number) # selects everything but litter_num
```

    ## # A tibble: 49 x 7
    ##    group gd0_weight gd18_weight gd_of_birth pups_born_alive pups_dead_birth
    ##    <chr>      <dbl>       <dbl>       <dbl>           <dbl>           <dbl>
    ##  1 Con7        19.7        34.7          20               3               4
    ##  2 Con7        27          42            19               8               0
    ##  3 Con7        26          41.4          19               6               0
    ##  4 Con7        28.5        44.1          19               5               1
    ##  5 Con7        NA          NA            20               6               0
    ##  6 Con7        NA          NA            20               6               0
    ##  7 Con7        NA          NA            20               9               0
    ##  8 Con8        NA          NA            20               9               1
    ##  9 Con8        NA          NA            20               8               0
    ## 10 Con8        28.5        NA            20               8               0
    ## # ... with 39 more rows, and 1 more variable: pups_survive <dbl>

``` r
select(litters_df, group) # selects the one variable, output = data frame
```

    ## # A tibble: 49 x 1
    ##    group
    ##    <chr>
    ##  1 Con7 
    ##  2 Con7 
    ##  3 Con7 
    ##  4 Con7 
    ##  5 Con7 
    ##  6 Con7 
    ##  7 Con7 
    ##  8 Con8 
    ##  9 Con8 
    ## 10 Con8 
    ## # ... with 39 more rows

``` r
#pull(litters_df, group) # selects the data from this one variable
```

Renaming Variables

``` r
select(litters_df, group_new = group, litter_number) # renames a variable
```

    ## # A tibble: 49 x 2
    ##    group_new litter_number  
    ##    <chr>     <chr>          
    ##  1 Con7      #85            
    ##  2 Con7      #1/2/95/2      
    ##  3 Con7      #5/5/3/83/3-3  
    ##  4 Con7      #5/4/2/95/2    
    ##  5 Con7      #4/2/95/3-3    
    ##  6 Con7      #2/2/95/3-2    
    ##  7 Con7      #1/5/3/83/3-3/2
    ##  8 Con8      #3/83/3-3      
    ##  9 Con8      #2/95/3        
    ## 10 Con8      #3/5/2/2/95    
    ## # ... with 39 more rows

``` r
rename(litters_df, group_new2 = group) # another way to change column name
```

    ## # A tibble: 49 x 8
    ##    group_new2 litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr>      <chr>                <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7       #85                   19.7        34.7          20               3
    ##  2 Con7       #1/2/95/2             27          42            19               8
    ##  3 Con7       #5/5/3/83/3-3         26          41.4          19               6
    ##  4 Con7       #5/4/2/95/2           28.5        44.1          19               5
    ##  5 Con7       #4/2/95/3-3           NA          NA            20               6
    ##  6 Con7       #2/2/95/3-2           NA          NA            20               6
    ##  7 Con7       #1/5/3/83/3-3/2       NA          NA            20               9
    ##  8 Con8       #3/83/3-3             NA          NA            20               9
    ##  9 Con8       #2/95/3               NA          NA            20               8
    ## 10 Con8       #3/5/2/2/95           28.5        NA            20               8
    ## # ... with 39 more rows, and 2 more variables: pups_dead_birth <dbl>,
    ## #   pups_survive <dbl>

Relocating variables

``` r
select(litters_df, litter_number, everything()) # reorders just one, keeping everything else
```

    ## # A tibble: 49 x 8
    ##    litter_number   group gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr>           <chr>      <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 #85             Con7        19.7        34.7          20               3
    ##  2 #1/2/95/2       Con7        27          42            19               8
    ##  3 #5/5/3/83/3-3   Con7        26          41.4          19               6
    ##  4 #5/4/2/95/2     Con7        28.5        44.1          19               5
    ##  5 #4/2/95/3-3     Con7        NA          NA            20               6
    ##  6 #2/2/95/3-2     Con7        NA          NA            20               6
    ##  7 #1/5/3/83/3-3/2 Con7        NA          NA            20               9
    ##  8 #3/83/3-3       Con8        NA          NA            20               9
    ##  9 #2/95/3         Con8        NA          NA            20               8
    ## 10 #3/5/2/2/95     Con8        28.5        NA            20               8
    ## # ... with 39 more rows, and 2 more variables: pups_dead_birth <dbl>,
    ## #   pups_survive <dbl>

``` r
relocate(litters_df, litter_number) # alternate way
```

    ## # A tibble: 49 x 8
    ##    litter_number   group gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr>           <chr>      <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 #85             Con7        19.7        34.7          20               3
    ##  2 #1/2/95/2       Con7        27          42            19               8
    ##  3 #5/5/3/83/3-3   Con7        26          41.4          19               6
    ##  4 #5/4/2/95/2     Con7        28.5        44.1          19               5
    ##  5 #4/2/95/3-3     Con7        NA          NA            20               6
    ##  6 #2/2/95/3-2     Con7        NA          NA            20               6
    ##  7 #1/5/3/83/3-3/2 Con7        NA          NA            20               9
    ##  8 #3/83/3-3       Con8        NA          NA            20               9
    ##  9 #2/95/3         Con8        NA          NA            20               8
    ## 10 #3/5/2/2/95     Con8        28.5        NA            20               8
    ## # ... with 39 more rows, and 2 more variables: pups_dead_birth <dbl>,
    ## #   pups_survive <dbl>

Learning assessment: In the pups data, select the columns containing
litter number, sex, and PD ears.

``` r
select(pups_df, litter_number, sex, pd_ears)
```

    ## # A tibble: 313 x 3
    ##    litter_number   sex pd_ears
    ##    <chr>         <dbl>   <dbl>
    ##  1 #85               1       4
    ##  2 #85               1       4
    ##  3 #1/2/95/2         1       5
    ##  4 #1/2/95/2         1       5
    ##  5 #5/5/3/83/3-3     1       5
    ##  6 #5/5/3/83/3-3     1       5
    ##  7 #5/4/2/95/2       1      NA
    ##  8 #4/2/95/3-3       1       4
    ##  9 #4/2/95/3-3       1       4
    ## 10 #2/2/95/3-2       1       4
    ## # ... with 303 more rows
