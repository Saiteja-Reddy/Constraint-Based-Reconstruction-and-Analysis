## Getting Started with RAVEN Toolbox

You can find the main website for RAVEN [here](https://github.com/SysBioChalmers/RAVEN).

The **RAVEN** Toolbox (**Reconstruction, Analysis, and Visualization of Metabolic Networks**) toolbox is a complete environment for reconstruction, analysis, simulation, and visualization of GEMs and runs within *MATLAB*.

The software has three main foci:
 1. Automatic reconstruction of GEMs based on protein homology
 2. Network analysis, modeling and interpretation of simulation results
 3. Visualization of GEMs using pre-drawn metabolic network maps.

### Installation Instructions

Below Instructions are for Linux Based Systems.

Prerequisites:

1. **MATLAB:** Ensure that you have a compatible and working MATLAB installation. No support is provided for versions older than R2013b. Find the latest version of MATLAB [here](https://in.mathworks.com/products/matlab.html).
2. **libSBML MATLAB API** (version 5.16 is recommended), which is utilised for importing and exporting GEMs in SBML format. Note: not needed if COBRA Toolbox is installed. You can download the binaries from [here](http://sbml.org/Software/libSBML).
3. Atleast one solver for linear programming, **Gurobi** can be installed in the same way as for COBRA Toolbox, which is free for academic licenses.
4. If you already have Cobratoolbox installed, which is prefered, you start the Cobratoolbox first, set the solver to *gurobi* using `changeCobraSolver` command and then launch RAVEN as discussed below for no compatibility issues.

To download/get RAVEN Toolbox, go to desired directory and  do

```
git clone https://github.com/SysBioChalmers/RAVEN
```


To run RAVEN Toolbox,

```
cd('[location]/RAVEN/installation'))
checkInstallation
```


See the demo on Ada below, when you want to start RAVEN Toolbox on MATLAB.


[![asciicast](https://asciinema.org/a/PcZHR0Rt7Xste3FOA6GkUHduQ.svg)](https://asciinema.org/a/PcZHR0Rt7Xste3FOA6GkUHduQ)


For the official RAVEN Toolbox Install Instructions - [refer here](https://github.com/SysBioChalmers/RAVEN/wiki/Installation).

[Back to Contents](../README.md)
