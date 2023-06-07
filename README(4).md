
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
-   Enter your username and your password
-   Copy the package in your working directory
-   Install it using this command line

``` r
install.packages("PoPcontinuity.tar.gz")
```

If the installation does not work using this command and/or if you have
an error message regarding your version of R, you may try this line :

``` r
install.packages("PoPcontinuity.tar.gz",repos=NULL,type="source",dependencies=TRUE)
```

Note that to make full use of the package, an access to the
<code>gmdp</code> partition is required.

During the installation you may see the following warnings :

<code> Warning messages: 
    1: In readLines(file, skipNul = TRUE, encoding= “bytes”) : cannot open compressed file
    ‘/usr/lib/R/site-library/dplyr/DESCRIPTION’, probable reason ‘No such file or directory’ 
    2: In readLines(file, skipNul = TRUE, encoding =“bytes”) : cannot open compressed file
    ‘/usr/lib/R/site-library/rlang/DESCRIPTION’, probable reason ‘No such file or directory’ 
</code>

It is probably due to later versions installed by GitHub or others, or
poorly constructed versions that are missing the DESCRIPTION files.  
Due to restricted permissions on the server I could not fix these issues
that *should not* affect the installation and the use of the package.

## Function create_files()

The function create_files() allows to obtain setting files ready to be
used for a SPLATCHE3 simulation from raw data files .  
You can retrieve all the information concerning the raw data file and
the setting files in the **Data** section.

This is a basic example which shows you how to use the command
create_file() to format setting files :

``` r
library(PoPcontinuity)
## basic example code
setting_files <- paste(system.file("extdata",package="PoPcontinuity"),"user_settings",sep="/")
create_files(setting_files)
```

This command performs the following steps :

-   Create a new folder called complete_settings
-   Format the data from user_settings and put it as setting files in
    complete_settings
-   Format the main setting file and put it outside of complete_settings
    so it can be used to launch a SPLATCHE3 simulation

This is an example of result (dynamic_F.txt) :

    #> [1] "1"                                             
    #> [2] "0 ./complete_settings/vegF_L1_time_1.txt Time1"

Note that all files are formatted together and not one by one as they
all need to be present and formatted the same way for the simulation to
work.

## Function launch_simulation()

The function launch_simulation() allows, to launch a SPLATCHE3
simulation using a setting folder and a setting file *located in the
working directory*.

If you did not use the function create_files() to build your setting
files, note that the launch_simulation() can only launch the simulation
using a file named simulation_param.txt.

This is a basic example which shows you how to use the command
launch_simulation() to perform a SPLATCHE3 simulation :

``` r
launch_simulations()
readLines(paste(system.file("extdata",package="PoPcontinuity"),"slurm-5814275.out",sep="/"))[12]
#> [1] "ALL SIMULATIONS AND PROGRAMS SUCCESSFULLY TERMINATED!"
```

In any cases, you should have in your working folder :

-   A SPLATCHE3 log file
-   A slurm file with a message indicated if the simulation was aborted

If the simulation ran successfully, you should have, in addition :

-   A SPLATCHE3 log file
-   A folder GeneticsOutput containing an .arp file (inside the settings
    folder)
-   A slurm file with a message indicating that the simulation
    terminated successfully

## Function raster_to_pdf()

The function raster_to_pdf() allows, to visualize in a PDF the raster
map used for the simulations.

This is an example which shows you how to use the command
raster_to_pdf() produce the visual output (the example may take quite
some time to execute):

``` r
map <- paste(system.file("extdata",package="PoPcontinuity"),"map.asc",sep="/")
raster_to_pdf(map)
#> The legacy packages maptools, rgdal, and rgeos, underpinning this package
#> will retire shortly. Please refer to R-spatial evolution reports on
#> https://r-spatial.org/r/2023/05/15/evolution4.html for details.
#> This package is now running under evolution status 0
```

<img width="393" alt="Screenshot 2023-06-07 164400" src="https://github.com/Sample1703/POPcontinuity/assets/118454951/1cf195fd-fe54-42a5-adbc-e9d83071b4ae">

    #> png 
    #>   2

Note that this function uses the package <code>raster</code>. In case of
trouble using the function, you can manually install this package using
the following command line :

``` r
install.packages("raster")
library(raster)
```

## Data

To use the function create_files() you have to provide a folder
containing both raw and already formatted data. Your file names have to
be similar to those presented below.

### Raw data files

The files described below are the raw data files that can be formatted
by the function create_files().  
After formatting, they can be used to launch simulations with SPLATCHE3

#### Arrival_cell.col

This file contains the coordinates of demes for which arrival times are
needed.  
It must be named **arrival_cell.col**.

The user is expected to have the raw data for this file as follow:

    #> Warning in readLines(paste(system.file("extdata", package = "PoPcontinuity"), :
    #> incomplete final line found on
    #> '/home-ltsp/tournay2/R/x86_64-pc-linux-gnu-library/4.3/PoPcontinuity/extdata/user_settings/arrival_cell.col'
    #> [1] "samp1,0,12,3"

#### Dens_init.txt

This file contains the locations, initial densities, etc of the initial
population(s).  
It must be named **dens_init.txt**.

The user is expected to have the raw data for this file as follow:

    #> Warning in readLines(paste(system.file("extdata", package = "PoPcontinuity"), :
    #> incomplete final line found on
    #> '/home-ltsp/tournay2/R/x86_64-pc-linux-gnu-library/4.3/PoPcontinuity/extdata/user_settings/dens_init.txt'
    #> [1] "Paleo,1000,22,9,0,0,0,0,0,0"

#### Dynamic_F.txt and dynamic_K.txt

The file dynamic_F.txt contains the path to the table making the
correspondence between vegetation categories and frictions values.  
It must be named **dynamic_F.txt**.

The user is expected to have the raw data for this file as follow:

    #> [1] "0 vegF_L1_time_1.txt Time1"

The file dynamic_K.txt contains the path to the table making the
correspondence between vegetation categories and carrying capacity.  
It must be named **dynamic_K.txt**.

The user is expected to have the raw data for this file as follow:

    #> Warning in readLines(paste(system.file("extdata", package = "PoPcontinuity"), :
    #> incomplete final line found on
    #> '/home-ltsp/tournay2/R/x86_64-pc-linux-gnu-library/4.3/PoPcontinuity/extdata/user_settings/dynamic_K.txt'
    #> [1] "0 vegK_L1_time_1.txt Time1"

#### Samples.sam

This file contains the coordinates, sizes, etc of the genetic samples.  
It must be named **samples.sam**.

The user is expected to have the raw data for this file as follow:

    #> Warning in readLines(paste(system.file("extdata", package = "PoPcontinuity"), :
    #> incomplete final line found on
    #> '/home-ltsp/tournay2/R/x86_64-pc-linux-gnu-library/4.3/PoPcontinuity/extdata/user_settings/samples.sam'
    #> [1] "sample1,30,0,12,22,400"

#### Simulation_param.txt

Each setting necessary to launch the simulation is called in this file
using the pair *SettingsName=value*.  
It must be named **simulation_param.txt**.

When calling path in this file, use this syntax:
<code>./complete_settings/file</code>.

This is an example of line from this file:

    #> [1] "./SettingsFolder/2.txt"

### Pre-formatted data files

In addition of the raw data files, the input folder has to contain
pre-formatted files.

#### Genetic_data.par

This file contains the definition of markers property.  
It must be named **genetic_data.par**.

The expected format for this file as follow:

    #> [1] "1 //Num chromosomes"                                                                                                                                                             
    #> [2] "#chromosome 1, //per Block:data type, number of loci, per generation recombination, per site mutation rates and transition rate (fraction of substitutions that are transitions)"
    #> [3] "1"                                                                                                                                                                               
    #> [4] "DNA    341   0.0000    0.0000078585   0.9841"

#### Map.asc

This file contains the Ascii file describing the initial world.  
It must be named **map.asc**.

#### Vegetation files

These files contain the friction (F) and carrying capacity (K) values
for each vegetation category. It must be named
**vegF_L1_time_1.txt**,**vegK_L1_time_1.txt** and
**vegK_L1_time_2.txt**.

This is an example of expected format for these files:

    #> [1] "1\t40\tTropical rainforest"

*For additional information regarding the setting files, you can consult
the SPLATCHE3 user manual :
<https://www.splatche.com/download/SPLATCHE3_User_Manual.pdf>*
