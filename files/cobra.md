## Getting Started with COBRA Toolbox

You can find the main website for COBRA [here](https://opencobra.github.io/cobratoolbox/stable/).

The **COnstraint-Based Reconstruction and Analysis Toolbox** is a MATLAB software suite for quantitative prediction of cellular and multicellular biochemical networks with constraint-based modelling. It implements a comprehensive collection of basic and advanced modelling methods, including reconstruction and model generation as well as biased and unbiased model-driven analysis methods.

### Installation Instructions

Below Instructions are for Linux Based Systems.

1. **MATLAB:** Ensure that you have a compatible and working MATLAB installation. No support is provided for versions older than R2014b. Find the latest version of MATLAB [here](https://in.mathworks.com/products/matlab.html).
2. **Git:** Check if you have a working installation of git.

  `` $ git --version ``

  If installed properly, this will return git  version number.

3. **Curl:** Check if you have a working installation of curl.

  `` $ curl --version ``

  If installed properly, this will return curl  version number.

4. **Solver Installation :** COBRA Toolbox supports the below solvers:
  - [TOMLAB](https://tomopt.com/)
  - [IBM ILOG CPLEX](https://www.ibm.com/in-en/marketplace/ibm-ilog-cplex)
  - [GUROBI](http://www.gurobi.com/)
  - [MOSEK](https://www.mosek.com/)

   Make sure that you install a compatible solver. The compatibility list is available [here](https://github.com/opencobra/cobratoolbox/blob/master/docs/source/installation/compatMatrix.rst).

   Do refer the COBRA docs for installation of various solvers.

    I've installed [GUROBI](http://www.gurobi.com/) on the *Institute's HPC ADA*.

    **Steps for Installation of GUROBI solver on *ADA*:**

    * Go to [GUROBI site](http://www.gurobi.com/), register with your Institute ID and login.
    * Go to [*Get Gurobi*](http://www.gurobi.com/downloads/download-center) and get an Academic License.
    * You can view your current liceses [here](https://user.gurobi.com/download/licenses/current).
    * Download the Gurobi optimizer from [here](http://www.gurobi.com/downloads/gurobi-optimizer).
    * Navigate to the directory where Gurobi was downloaded and do

    ``` bash
    $ tar -xvzf <archive>.tar.gz
    $ cd gurobi<ver-num>/linux64/bin
    $ grbgetkey YOUR-LICENSE-KEY-FROM-SITE

    In which directory would you like to store the Gurobi license key file?
    [hit Enter to store it in /home/<userid>]:

    $ vim ~/.bashrc
    ```
    To your bashrc file add the below lines:

    ```
    export GUROBI_HOME="/path-to-gurobi/gurobi<ver>/"
export PATH="${PATH}:${GUROBI_HOME}/bin"
export LD_LIBRARY_PATH="${LD_LIBRARY_PATH}:${GUROBI_HOME}/lib"
export GUROBI_PATH="${GUROBI_HOME}"
export GRB_LICENSE_FILE="/path-to-gurobi/gurobi<ver>/linux64/gurobi.lic"
    ```
    The last line for the path of License File will be different depending on where you saved the license when you ran the command ``grbgetkey``.

    ** Note: ** For HPC machines like Ada, the license is for one node at a time. So if you register GUROBI once for a node make sure you are using that same node for computation. You have to install a license to each node if you want to use GUROBI with any node. *Make sure you change the license file path whenever you are switching nodes.*

  5. Now, download Cobratoolbox itself.

    ```
    git clone --depth=1 https://github.com/opencobra/cobratoolbox.git cobratoolbox
    ```

 6. Launch MATLAB. On HPC, first get an interactive session/node, load the MATLAB module and then launch MATLAB.
 7. Change to the folder to cobratoolbox/ and run from MATLAB.

    ```
    >>> initCobraToolbox
    ```

    See the demo on Ada below, when you start Cobra Toolbox on MATLAB.

    [![asciicast](https://asciinema.org/a/wwoPFvkmTSN7sil5Bz2f6da6P.svg)](https://asciinema.org/a/wwoPFvkmTSN7sil5Bz2f6da6P)

  8. **(Optional) Test the installation:** You may test your installation by running from MATLAB

  ```
    >> testAll
  ```

For the official COBRA Toolbox Install Instructions - [refer here](https://opencobra.github.io/cobratoolbox/stable/installation.html).

[Back to Contents](../README.md)
