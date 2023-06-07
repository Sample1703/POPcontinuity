
<!-- README.md is generated from README.Rmd. Please edit that file -->

# POPcontinuity

<!-- badges: start -->
<!-- badges: end -->

The goal of POPcontinuity is to :

-   Use raw data to format setting files
-   Launch SLATCHE3 simulations
-   Offer a visual representation of a raster map in a PDF file

## Installation

To use the package POPcontinuity you have to be connected to the server
of the University of Geneva. You can follow the following procedure :

-   Click on this link: <http://biant-lsrv05.unige.ch:2022/>
-   Copy the package in your working directory
-   Install it using this command line

``` r
install.packages("POPcontinuity.tar.gz")
```

Note that to make full use of the package, an access to the gmdp
partition is required.

## Example

This is a basic example which shows you how to format setting files:

``` r
library(POPcontinuity)
## basic example code
setting_files <- paste(system.file("extdata",package="POPcontinuity"),"user_settings",sep="/")
create_files(setting_files)
#> Warning in write.table(df, file = paste0("complete_settings/", filename), :
#> appending column names to file

#> Warning in write.table(df, file = paste0("complete_settings/", filename), :
#> appending column names to file

#> Warning in write.table(df, file = paste0("complete_settings/", filename), :
#> appending column names to file
```

This command performs the following steps :

-   Create a new folder called complete_settings
-   Format the data from user_settings and put it as setting files in
    complete_settings
-   Format the main setting file and put it outside of complete_settings
    so it can be used to launch a SPLATCHE3 simulation

This is an example of result :

    #> [1] "0 vegF_L1_time_1.txt Time1"
