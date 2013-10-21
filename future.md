---
layout: default
title: Future developments
---

# Future developments

Mosaic is still a young project, many important features still remain
to be defined and implemented. This page gives an overview of what is
planned and currently being worked on, starting with the most concrete
plans and moving on to more and more vague ideas.

## Software

At the moment, the only support code for Mosaic is written in Python.
Since much molecular simulation software is written in C, C++ or
Fortran, in particular for the the CPU intensive algorithms, a
Mosaic C library is the top item on the priority list. It will probably
support only the HDF5 file format, at least initially, because it is
the only file format suitable for high-performance applications.


## Simple stuff

A few data items are straightforward to define and implement, it just
needs to be done. Mosaic should thus soon include:

 * atom pair lists (e.g. for distance constraints)
 * rigid-body definitions
 * normal modes


## Trajectories

Trajectories are produced by various common algorithms. Some of them
produce a trajectory with a time axis (Molecular Dynamics, Brownian
Dynamics, ...), whereas others produce a sequence of configurations
without the connotation of evolution in time (e.g. most Monte Carlo
techniques). Trajectories are read by analysis programs that compute
physical observables from a simulation, and also by visualization
programs for creating animations.

Trajectory storage is not trivial because of the large amounts of data
that must be handled. Both file size and access time are critical
issues.  Of the current Mosaic file formats, only HDF5 is an
appropriate choice for real-life trajectory data for this reason.

Another consideration when defining trajectory storage is flexibility.
Most trajectory-generating algorithms produce not only a sequence of
configurations, but also of additional data such as velocities,
forces, energies, etc. A trajectory format should not impose
limitations on what can be stored, but also clearly identify the
stored quantities to ensure a correct interpretation.

We are currently exploring [H5MD](http://nongnu.org/h5md/draft.html),
a proposed HDF5-based format for trajectories that covers a wider
range of simulation techniques than Mosaic, but does not by itself
provide a description of the molecular system. It looks feasible
to add a few Mosaic datasets to an H5MD trajectory and obtain
a format that fulfills all the requirements discussed above.

## Force fields

A force field is a recipe for computing potential energies (and their
derivatives) for a given system in a given configuration. In terms of
Mosaic data, a force field is a mathematical function of two
parameters: a universe and a configuration. It is also common to have
additional problem-specific force field terms, such as restraints.

Since a force field is an arbitrary mathematical function, its
specification requires a Turing-complete programming language.
However, it is not very practical to use a general-purpose language
such as C, Fortran, or Python for defining force fields. The force
field specification would be complicated, and simulation programs
would have to implement compilers or interpreters for these languages.
A better approach is to define a
[domain-specific language](http://en.wikipedia.org/wiki/Domain-specific_language)
(DSL) tailor-made for describing force fields. Such a DSL can exploit
the fact that commonly used force fields are combinations of a very small
number of simple mathematical functions.


## Volumetric data

Volumetric data takes the form of a grid in space with a numerical
value associated with each grid point. It is most frequently used
for experimental data (e.g. electron density maps in crystallography
and electron microscopy), but can also be computed from a simulation
(e.g. a mass or charge density).


## Experimental data

Often the interpretation of experimental data is based on molecular
simulations, for example in molecular structure determination from
crystallography or NMR. For such applications, it should be possible
to store the experimental input data in Mosaic as well.


## Conventions

Mosaic defines appropriate data structures for molecular simulation
data, but leaves a lot of freedom as to how they should be used.
Additional conventions are required to make sure that common combinations
of Mosaic data items are handled consistently by all programs.

As an example, consider a crystallographic structure as stored in the
PDB. Its storage in Mosaic requires a universe, a configuration, and
two properties for displacement factors and occupancies. A convention
fixes the remaining details: the names of the data items, whether to
always store occupancies or only if at least one of them is less than
1, etc. [This particular convention]
(http://mosaic-data-model.github.io/mosaic-specification/pdb_convention.html)
is already part of the Mosaic specification.
