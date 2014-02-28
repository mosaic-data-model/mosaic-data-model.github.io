---
layout: default
title: MOSAIC
---

# MOSAIC - the MOlecular SimulAtion Interchange Conventions

Mosaic is a modular set of data models and file formats for molecular
simulation. The two main goals of the Mosaic project are

* Provide a way to store a very detailed description of a molecular
  simulation for publication and archiving, according to the
  principles of
  [Reproducible Research](http://en.wikipedia.org/wiki/Reproducibility).

* [Facilitate the exchange of data](molecular_simulation.html)
  between molecular simulation software packages.

For more background information, see the
[Mosaic design criteria](design_criteria.html) and the paper
["MOSAIC: A Data Model and File Formats for Molecular Simulations"](http://dx.doi.org/10.1021/ci400599y). For
those who don't have a subscription to the Journal of Chemical
Information and Modeling, the paper is available for free (limited to
50 downloads during the first year) through the
[ACS Articles on Request service](http://pubs.acs.org/articlesonrequest/AOR-dADBta6jVTVtVb6bbGmJ) (registration required).

## Contributing to Mosaic development

If you would like to contribute to the development of Mosaic, please
join the [mailing list](https://groups.google.com/d/forum/mosaic-developers).

## Current status

Mosaic has been used successfully in real research projects and
publications. [Future developments](future.html) of the specification
are most likely to be extensions. The Python library should be
considered alpha-level, because details of the interface can still
change.


## Mosaic overview

Mosaic currently defines five kinds of data items:

* A *universe* is the definition of the system topology (periodic
  boundary conditions etc.) and the chemical structure of its
  molecules (fragment hierarchy, bond network). The universe
  definition is the central data structure in Mosaic, because it
  permits the correct interpretation of the other data types.

* A *configuration* provides a set of positions for all atoms plus
  the geometric parameters of the simulation cell if periodic boundary
  conditions are used.

* A *property* stores one value for each atom in a universe. The
  value can be an N-dimensional array of integers or floats. Property
  items are very versatile. They can be used to store masses, charges,
  velocities, forces, and much more.

* A *label* stores a text string for each atom in a universe. Labels
  are used for storing atom names, atom types, and similar
  information.

* A *selection* stores a subset of the atoms or sites in a universe.
  Selections are used for identifying parts of the system (e.g. solvent,
  active site, ...).

The Mosaic data model defines how these data items are expressed in
terms of basic data items (integers, floats, text strings) and basic
data structures (lists, arrays, trees, ...). The Mosaic file format
definitions describe how the data model is represented in files.
Conversion between different Mosaic file formats is exact; no
information is lost and no information needs to be deduced.

Currently there are two Mosaic file formats:

* The [HDF5](http://www.hdfgroup.org/HDF5/) format provides compact
  and efficient binary storage in a platform-independent way.
  HDF5 is the right choice for large data sets (e.g. Molecular Dynamics
  trajectories) and can be interfaced easily with programs written
  in C, C++, or Fortran because of its array-based nature.

* The [XML](http://www.w3.org/XML/) format provides text-based storage
  that can be inspected and modified with any plain-text editor. A large
  number of XML processing programs and XML libraries for all major
  programming languages make it easy to do non-numerical processing
  on molecular systems.

## The Mosaic Python library

The current Mosaic Python library implements three
in-memory representations of the Mosaic data model and I/O in the two
supported file formats. It also contains an import module for
structures from the [Protein Data Bank](http://www.wwpdb.org/).  A
simple command-line tool can convert between the file formats and
write imported PDB structures to Mosaic files.

## Related projects

* The [Rich Molecular Format](http://salilab.github.com/rmf/)
  (RMF) shares some aspects of Mosaic, in particular the hierarchical
  representation of molecules. However, the focus seems different
  (molecular structures with annotations for visual representation
  and experimental information), leading to different design choices.

## Acknowledgements

Mosaic development was supported by the
[Agence Nationale de la Recherche](http://www.agence-nationale-recherche.fr/)
under
[contract N° ANR-2010-COSI-001-01](http://dirac.cnrs-orleans.fr/sputnik/home/).
