.. _R_package_management:

R package management
====================

Introduction
------------

Most of the useful R packages can be installed separately. Some of those are 
part of the centrally installed R modules. However, given the astounding number of 
packages, it is not sustainable to install each and everyone of them system wide. 
Fortunately, it is very easy for users to install R packages themselves.
If you do encounter problems when doing so, do not hesitate to contact support.

.. _r_package_management_standard_lib:

Standard R package installation
-------------------------------

Setting up your own package repository for R is straightforward.

#. Load the appropriate R module, i.e., the one you want the R package
   to be available for::

      $ module load R/3.2.1-foss-2014a-x11-tcl

#. Start R and install the package (preferably in your $VSC_DATA directory)::

      > install.packages("DEoptim", lib="/data/leuven/304/vsc30468/R/")

#. Alternatively you can download the desired package::

      $ wget cran.r-project.org/src/contrib/Archive/DEoptim/DEoptim_2.0-0.tar.gz

      and install it with::
  
      $ R CMD INSTALL DEoptim_2.0-0.tar.gz  -l /$VSC_DATA/R/
      
#. These packages might depend on the specific R version, so you may
   need to reinstall them for the other version.
   
Some R packages depend on libraries installed on the system.  In that case,
you first have to load the modules for these libraries, and only then proceed
to the R package installation.  For instance, if you would like to install
the `gsl` R package, you would first have to load the module for the GSL
library, .e.g., ::

   $ module load GSL/2.5-GCC-6.4.0-2.28

.. note::

  R packages often depend on the specific R version they were installed
  for, so you may need to reinstall them for other versions of R.

.. _r_package_management_conda:

Installing R packages using conda
---------------------------------

.. note::

    Conda packages are incompatible with the software modules.
    Usage of conda is discouraged in the clusters at UAntwerpen, UGent,
    and VUB.

The easiest way to install and manage your own R environment(s) is conda.

.. _install_miniconda_r:

Installing Miniconda
~~~~~~~~~~~~~~~~~~~~

If you have Miniconda already installed, you can skip ahead to the next
section, if Miniconda is not installed please follow our :ref:`guide to installing miniconda <install_miniconda_python>`.

.. _create_r_conda_env:

Creating an environment
~~~~~~~~~~~~~~~~~~~~~~~

First, ensure that the Miniconda installation is in your PATH
environment variable. The following command should return the full path
to the conda command::

   $ which conda

If the result is blank, or reports that conda can not be found, modify
the \`PATH\` environment variable appropriately by adding miniconda's bin
directory to PATH.

The next step is to create a new conda environment which can be done as follows::

   $ conda search -c conda-forge r-base  # select one of available versions for the step below
   $ conda create -n science -c conda-forge r-base=<version> r-essentials
   

This command creates a new conda environment called "science", and installs your prefered R 
version from the conda-forge channel as well as the r-essentials bundle which includes number
of commonly used R packages such as ggplot2, glmnet, dplyr, tidyr, and shiny.

.. note::

   A lot of bioconda and bioconductor packages are not in sync with their dependencies, therefore you may need to create a separate environment for each of those packages to avoid conflicts.

Working with the environment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To work with an environment, you have to activate it. This is done with,
e.g.,

::

   $ source activate science

Here, science is the name of the environment you want to work in.


Install an additional package
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To install an additional package, e.g., \`rodbc`, first ensure that the
environment you want to work in is activated.

::

   $ source activate science

Next, install the package:

::

   $ conda install -c conda-forge r-rodbc

Note that conda will take care of all dependencies, including non-R
libraries. This ensures that you work in a consistent environment.

Updating/removing
~~~~~~~~~~~~~~~~~

Using conda, it is easy to keep your packages up-to-date. Updating a
single package (and its dependencies) can be done using:

::

   $ conda update r-rodbc

Updating all packages in the environment is trivial:

::

   $ conda update --all

Removing an installed package:

::

   $ conda remove r-mass

Deactivating an environment
~~~~~~~~~~~~~~~~~~~~~~~~~~~

To deactivate a conda environment, i.e., return the shell to its
original state, use the following command

::

   $ source deactivate

More information
~~~~~~~~~~~~~~~~

Additional information about conda can be found on its `documentation site <https://docs.conda.io/en/latest/>`__.

For installing R packages from github or other repositories see also :ref:`R devtools<r_devtools>`:
