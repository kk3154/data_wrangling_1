Tidy Data Lecture
================

## pivot longer

Load the PULSE data.

``` r
pulse_df = 
  read_sas("data/public_pulse_data.sas7bdat") %>% 
  janitor::clean_names()
```

Data is currently in wide format - columns for baseline, 1 mo, 6 mo, 12
mo, etc.

Using pivot function

``` r
pulse_tidy = 
  pulse_df %>% 
  pivot_longer(
    bdi_score_bl:bdi_score_12m,
    names_to = "visit", 
    names_prefix = "bdi_score_", # removes prefix from beginning of the var name
    values_to = "bdi"
  ) %>% 
  mutate(
    visit = replace(visit, visit == "bl", "00m"),
    visit = factor(visit) # converting visit variable to a factor
  )
```
