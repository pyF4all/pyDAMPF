.. figure:: https://github.com/willymenacho/pyDAMPF/blob/pyDAMPF_INTERFACE/logo.png

pyDAMPF: a Python package for modeling mechanical and electrostatic properties of hygroscopic materials under interaction with a nanoprobe
======================================================

pyDAMPF is a tool oriented to the Atomic Force Microscopy (AFM) community, which allows the simulation of the physical properties of materials under variable relative humidity (RH).

The computing engine is written in Fortran in order to reuse physics code and wrapped to Python to interoperate with high-level packages. We also introduce an in-house multi-thread approach of the pyDAMPF code, which compares for various computing architectures (PC, Google Colab and a HPC facility) very favorable in comparison to a former AFM simulator. 


Users can use the existing cantilever database to perform their simulations or add-up further models. There are three ways of running pyDAMPF:

- serial (uses a single thread)
- multi-thread (unix based computer)
- multi-thread (SLURM based computer)

Documentation and learning material is also available in the form of:


- An introduction to compyle in the context of writing a parallel molecular
  dynamics simulator is in our `SciPy 2020 paper
  <http://conference.scipy.org/proceedings/scipy2020/CHANGE_OUR_DIRECTORY>`_.

- You may also try Compyle online for free on a `Google Colab notebook`_.

.. _Google Colab notebook: https://colab.research.google.com/drive/1ZM_aQsuYWUD2gnhcIhngpypJ6m1MbFxE?usp=sharing

- A short tutorial on how to use the `pyDAMPF interface`_.
.. _pyDAMPF interface: https://youtu.be/RqBXJc4Augw

Installation
-------------

Compyle is itself largely pure Python but depends on numpy_, matplotlib_, and plotly_

You should be able to download pyDAMPF  by doing::

  $ git clone https://github.com/govarguz/pyDAMPF/


.. _numpy: http://www.numpy.org
.. _matplotlib: https://matplotlib.org
.. _plotly: https://plotly.com


pyDAMPF has a numerical kernel in fortran so it is necessary to install the correct 
version.

  $ sudo apt-get update
  
  $ sudo apt-get install gfortran-7-multilib


Compilation with f2py: This step is only required once,and depends on the computer 
architecture, by using f2py with the file pyDAMPF.f90 within the folder
EXECUTE_pyDAMPF, the code for this reads

  $ f2py -c --fcompiler=gnu95 pyDAMPF.f90 -m mypyDAMPF
  
  $ cp *.so ~/pyDAMPF/EXECUTE_pyDAMPF/pyDAMPF_BASE/nrun/
  
  $ cp *.so ~/pyDAMPF/EXECUTE_pyDAMPF/pyDAMPF_BASE/nrun/runa
  
 

Generate Cases
-------------

Once we have obtained the numerical code as Python modules we generate the 
tempall.txt file which contains all the necessary parameters and variables for 
the pyDAMPF execution.

  $ python3 inputs_processor.py

Execute pyDAMPF
-------------

We need to choose the execution mode which can be serial or parallel. 
Whereby parallel refers within this first version of the code to multi-threading
capabilities only.

Serial method: Our in-house development creates an individual folder for 
each simulation case,which can be executed in one thread.

  $ python3 serial_method.py
  
Parallel method: 

  This method comprises two parts:

  First a function which takes care of the bookkeeping of 
  cases and folders:

    $ python3 parallel_method.py <number of threads>
  
  The second part of the parallel method will execute pyDAMPF, which contains
  at the same time two scripts. One for executing pyDAMPF in a common UNIX 
  based desktop or laptop. 

    $ python3 job_parallel_computer.py <number of threads>

  While the second is a python script which generated SLURM code to launch
  jobs in HPC facilities

    $ python3 job_parallel_cluster.py <number of threads>
  
Analysis
-------------  
  
Once the pyDAMPF simulation is finished,  pyDAMPF has two ways of analyzing the data.

The graphical analysis:

  $ python3 Graphical_analysis.py

The quantitative analysis:

  $ python3 Quantitative_analysis.py
  
Alternatively we offer for both cases an interactive environment in jupyter notebook. 

  $ pip install tabloo
  
  $ jupyter notebook Graphical_analysis.ipynb
  
  $ jupyter notebook Quantitative_analysis.ipynb
  
  

Example
---------

To relate to the use of pyDAMPF you can access `Google Colab notebook`_.

