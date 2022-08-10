WE used :
GNU Fortran (Ubuntu 7.5.0-6ubuntu2) 7.5.0
Python 3.9.7

||||||||||||||||||||||||||| FOR f2py COMPILATION|||||||||||||||||||||||||||||

IN THE TERMINAL:

cd EXECUTE_pyDAMPF/

f2py -c --fcompiler=gnu95 pyDAMPF.f90 -m mypyDAMPF
cp *.so ./pyDAMPF/EXECUTE_pyDAMPF/pyDAMPF_BASE/nrun/
cp *.so ./pyDAMPF/EXECUTE_pyDAMPF/pyDAMPF_BASE/nrun/runa

|||||||||||||||||||||  pyDAMPF USE  ||||||||||||||||||||||||||||||||

TABLOO: https://pypi.org/project/tabloo/
PLOPLY: https://pypi.org/project/plotly/
KALEIDOS: https://plotly.com/python/static-image-export/

SO IN THE TERMINAL :

pip install tabloo
pip install plotly
pip install kaleido

|||||||||||||||||||||  FOR EXECUTE pyDAMPF  ||||||||||||||||||||||||||||||||

IN THE TERMINAL:

jupyter notebook interfaz_v1.ipynb
			
			
YOUTUBE TUTORIAL:

https://youtu.be/RqBXJc4Augw

||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||


