[![PyPI version shields.io](https://img.shields.io/pypi/v/trusspy.svg)](https://pypi.python.org/pypi/trusspy/) [![Documentation Status](https://readthedocs.org/projects/trusspy/badge/?version=latest)](https://trusspy.readthedocs.io/en/latest/?badge=latest) [![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0) ![Made with love in Graz (Austria)](https://img.shields.io/badge/Made%20with%20%E2%9D%A4%EF%B8%8F%20in-Graz%20(Austria)-0c674a) [![codecov](https://codecov.io/gh/adtzlr/trusspy/branch/main/graph/badge.svg?token=__token__)](https://codecov.io/gh/adtzlr/trusspy) [![DOI](https://zenodo.org/badge/xyz.svg)](https://zenodo.org/badge/latestdoi/xyz) ![Codestyle black](https://img.shields.io/badge/code%20style-black-black)

**TrussPy** is a 3D **Truss**-Solver written in **Py**-thon which is capable of material and geometric nonlinearities. It uses an object-oriented approach to structure the code in meaningful classes, attributes and methods. TrussPy contains both multistep functionality (multiple loadcase analysis with sequenced external forces) and an adaptive method to control incremental stepwidths. Input files may be written in Excel or directly in Python. A simple post-processing inside TrussPy is directly available via Matplotlib. Model Plots whether in undeformed or deformed configuration with optional contour plots on element forces are easy to show. They may also be generated for a series of increments and saved as a GIF Movie. Last but not least History (a.k.a. x-y) Plots for a series of increments or Path Plots along a given node path may be generated for nodal properties (displacements, forces) or global quantities like the Load-Proportionality-Factor (LPF).
   
Official Documentation: http://trusspy.readthedocs.io/

# Installation

Use `pip` to install TrussPy

```
pip install trusspy
```

# Example

```python
import trusspy as tp

M = tp.Model()

# create nodes
with M.Nodes as MN:
    MN.add_node( 1, (0,0,0) )
    MN.add_node( 2, (1,0,0) )

# create element
with M.Elements as ME:
    ME.add_element( 1, [1,2] )
    ME.assign_material('all', [1])
    ME.assign_geometry('all', [1])

# create displacement (U) boundary conditions
with M.Boundaries as MB:
    MB.add_bound_U( 1, (0,0,0) )
    MB.add_bound_U( 2, (1,0,0) )

# create external forces
with M.ExtForces as MF:
    MF.add_force( 2, (1,0,0) )

# build model, run, show results
M.build()
M.run()

# plot results
M.plot_model()
M.plot_show()
```
	
# Online Notebook

Try TrussPy without installation in an [Interactive Online Notebook](https://mybinder.org/v2/gh/adtzlr/trusspy/master?filepath=tests%2Fe101_nb_interactive.ipynb).