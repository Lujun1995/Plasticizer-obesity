Plastic
================
Yun He, Jun Lu, Chu Yu, Chunxiao Zhai, Haoran Hu
11/21/2018

Overview
--------

Read and clean the data
-----------------------

``` r
phthte_file_name = tibble(file_name = list.files("./data/PHTHTE/"))

phthte =
  phthte_file_name %>% 
  mutate(map(str_c("./data/PHTHTE/", file_name), ~read.xport(.x))) %>% 
  unnest() 
    
demo_file_name = tibble(file_name_2 = list.files("./data/DEMO/"))

demo = 
    demo_file_name %>% 
    mutate(map(str_c("./data/DEMO/", file_name_2), ~read.xport(.x))) %>% 
    unnest()

phthe_demo = inner_join(demo, phthte, by = "SEQN") %>% 
    select(file_name, gender = RIAGENDR, age = RIDAGEYR, race = RIDRETH1, weight = WTMEC2YR, 
           income = INDFMPIR, URXCNP, URXCOP, URXECP) %>% 
    mutate(phthe = log(URXCNP + URXCOP + URXECP),
           phthe_combin = ifelse(phthe > 3.73, 1 ,0)) 
```

Exploratory analysis
--------------------

Tendency analysis
-----------------

Population compare
------------------
