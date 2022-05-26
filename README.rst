pyDAMPF: a Python package for modeling mechanical properties of hygroscopic materials under interaction with a nanoprobe
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
  <http://conference.scipy.org/proceedings/scipy2020/compyle_pr_ab.html>`_.

- `Compyle poster presentation <https://docs.google.com/presentation/d/1LS9XO5pQXz8G5d27RP5oWLFxUA-Fr5OvfVUGsgg86TQ/edit#slide=id.p>`_

- You may also try Compyle online for free on a `Google Colab notebook`_.

.. _Google Colab notebook: https://colab.research.google.com/drive/1SGRiArYXV1LEkZtUeg9j0qQ21MDqQR2U?usp=sharing


Installation
-------------

Compyle is itself largely pure Python but depends on numpy_.

You should be able to download pyDAMPF  by doing::

  $ git clone https://github.com/govarguz/pyDAMPF/


.. _numpy: http://www.numpy.org

pyDAMPF has a numerical kernel in fortran so it is necessary to install the correct 
version.

  $ sudo apt-get update
  $ sudo apt-get install gfortran-7-multilib

Compilation with f2py: This step is only required once,and depends on the computer 
architecture, the code for this reads

  $ f2py -c --fcompiler=gnu95 pyDAMPF.f90 -m mypyDAMPF
  



A simple example
----------------

Here is a very simple example::

   from compyle.api import Elementwise, annotate, wrap, get_config
   import numpy as np

   @annotate
   def axpb(i, x, y, a, b):
       y[i] = a*sin(x[i]) + b

   x = np.linspace(0, 1, 10000)
   y = np.zeros_like(x)
   a, b = 2.0, 3.0

   backend = 'cython'
   get_config().use_openmp = True
   x, y = wrap(x, y, backend=backend)
   e = Elementwise(axpb, backend=backend)
   e(x, y, a, b)

This will execute the elementwise operation in parallel using OpenMP with
Cython. The code is auto-generated, compiled and called for you transparently.
The first time this runs, it will take a bit of time to compile everything but
the next time, this is cached and will run much faster.

If you just change the ``backend = 'opencl'``, the same exact code will be
executed using PyOpenCL_ and if you change the backend to ``'cuda'``, it will
execute via CUDA without any other changes to your code. This is obviously a
very trivial example, there are more complex examples available as well.


Examples
---------

Some simple examples and benchmarks are available in the `examples
<https://github.com/pypr/compyle/tree/master/examples>`_ directory.

You may also run these examples on the `Google Colab notebook`_
