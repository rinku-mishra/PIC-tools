# PIC tools

In a standard workflow each project is given a project folder (e.g. `Chamber`),
and within this folder there's a folder for each simulation run. The naming
convention of the run folders is specific to each project, but as a rule it is
convenient to encode values of parameters being varied in the name. E.g., if
the density and temperature varies, a folder could be named `Step1_10n_1500K`
to indicate a density of `10e10` and a temperature of `1500K`. This will allow
parsing of the folder name for batch post-processing of all folders. I
sometimes use a prefix such as `Step1` to indicate that this is the first
attempt at getting all the parameters right, and so forth.

I typically store everything related to a given simulation within its run
folder: input files, output files, post-processed results, etc. That makes it
easy to backtrack to exactly which input parameters were used for a given
result. The files have standardized names, such that post-processing scripts
only need the path to the folder as an argument. The scripts can read from
multiple files, and save new results into the folder with standardized name.
One may run consecutive scripts if necessary. The scripts are typically not
general, but customized to each project.

### disprel_split.py
``` bash
usage: disprel_split.py [-h] [--i I] [--periodic PERIODIC] [--yLoc YLOC] [--sN SN] [--plot PLOT]

Plasma Dispersion Processor

optional arguments:
  -h, --help           show this help message and exit
  --i I                Path to E-field data (String)
  --periodic PERIODIC  Period System in Y (True/False)
  --yLoc YLOC          Choose Y location in bounded system (integer between 0,Ny)
  --sN SN              No. of chuncks you want to split the processed file (integer between 1,N)
  --plot PLOT          Plot the figure (True/False)
```
#### Example
``` bash
./disprel_split.py --i <path_to_data> --periodic True --sN 2 --plot True
```
