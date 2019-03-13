Workout
================
Amir Hisham
3/10/2019

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

    ## [[1]]
    ## [1] "readr"     "stats"     "graphics"  "grDevices" "utils"     "datasets" 
    ## [7] "methods"   "base"     
    ## 
    ## [[2]]
    ## [1] "ggplot2"   "readr"     "stats"     "graphics"  "grDevices" "utils"    
    ## [7] "datasets"  "methods"   "base"     
    ## 
    ## [[3]]
    ##  [1] "dplyr"     "ggplot2"   "readr"     "stats"     "graphics" 
    ##  [6] "grDevices" "utils"     "datasets"  "methods"   "base"     
    ## 
    ## [[4]]
    ##  [1] "knitr"     "dplyr"     "ggplot2"   "readr"     "stats"    
    ##  [6] "graphics"  "grDevices" "utils"     "datasets"  "methods"  
    ## [11] "base"

Trials and Errors: Same Goes with the Warriors
==============================================

> He who is not courageous enough to take risks will accomplish nothing in life - Muhammad Ali

All great sportsmen have one thing in common. They have all failed at some point in their lives. The same thing can be said about the Warriors players for the 2016 season. We will look at five key players and analyze their shooting styles, and pointers to see how well they did in the 2016 season.

``` r
knitr::include_graphics('~/Desktop/STAT_133/workout01/images/gsw-shot-charts.pdf')
```

The figures above lay out every shot made by the five key players. As we see, Klay Thompson and Steph Curry made the most shots, with Kevin Durant, Draymond Green, and Andre Iguodala came out third, forth and fifth players respectively in the number of shots. Knowing this, basketball players have to try harder to make more shots because all great players have that same characteristic. Note that this is for the 2016 season alone. If all the years are combined and analyzed, we would see the entire figures above fully colored with either green or red!

The figure below shows what happens if we dissect further and only look at Steph Curry figure alone.

``` r
knitr::include_graphics('~/Desktop/STAT_133/workout01/images/steph-curry-shot-chart.pdf')
```

Based on this figure, we can see clearly where the shots were made, and whether or not he actually made the shot. As you can see, there is no definite x and y coordinates on the diagram where the shots made are completely green or red. We can see however that as he gets closer to the ring, the amount of green dots seem to be higher. However, by looking at the general overview of the diagram, no matter where the shot was made, there is no definite answer as to whether the shot actually passed or not. This reinforces the idea of the law of averages whereby if the player keeps on trying, they are bound to make the shot. Hence, other players should not hesitate to try and see if they could make the shots, even though they know that they might miss it. It's the effort that counts.

However, we should take into account their experience too when coming up with the conclusion that other basketball players should try more because the difference between Steph Curry and Klay Thomson with other basketball players is that they can actually score more points than others because of their talent. While we cannot hypothesise this by just looking at the diagram, let's make a hypothesis that they were only able to make more shots because of their talents for now even though we may not sure if the hypothesis is true.

``` r
shooting_two <-
  summarise(
    group_by(binded_data, name),
    total = sum(shot_type == "2PT Field Goal"),
    made = sum(shot_type == "2PT Field Goal" & shot_made_flag == "shot_yes"),
    perc_made = made/total)
shooting_two
```

    ## # A tibble: 5 x 4
    ##   name           total  made perc_made
    ##   <chr>          <int> <int>     <dbl>
    ## 1 Andre Iguodala   346   171     0.494
    ## 2 Draymond Green   346   171     0.494
    ## 3 Kevin Durant     643   390     0.607
    ## 4 Klay Thomson     640   329     0.514
    ## 5 Steph Curry      563   304     0.540

``` r
shooting_three <-
  summarise(
    group_by(binded_data, name),
    total = sum(shot_type == "3PT Field Goal"),
    made = sum(shot_type == "3PT Field Goal" & shot_made_flag == "shot_yes"),
    perc_made = made/total)
shooting_three
```

    ## # A tibble: 5 x 4
    ##   name           total  made perc_made
    ##   <chr>          <int> <int>     <dbl>
    ## 1 Andre Iguodala   232    74     0.319
    ## 2 Draymond Green   232    74     0.319
    ## 3 Kevin Durant     272   105     0.386
    ## 4 Klay Thomson     580   246     0.424
    ## 5 Steph Curry      687   280     0.408

``` r
shooting_overall <-
  summarise(
    group_by(binded_data, name),
    total = sum(shot_type == "3PT Field Goal" | shot_type == "2PT Field Goal"),
    made = sum((shot_type == "3PT Field Goal" | shot_type == "2PT Field Goal") & shot_made_flag == "shot_yes"),
    perc_made = made/total)
shooting_overall
```

    ## # A tibble: 5 x 4
    ##   name           total  made perc_made
    ##   <chr>          <int> <int>     <dbl>
    ## 1 Andre Iguodala   578   245     0.424
    ## 2 Draymond Green   578   245     0.424
    ## 3 Kevin Durant     915   495     0.541
    ## 4 Klay Thomson    1220   575     0.471
    ## 5 Steph Curry     1250   584     0.467
