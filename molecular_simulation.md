---
layout: default
title: Molecular simulations
---

# Molecular simulations with MOSAIC

## Preparing and running simulations

Mosaic has the potential to change in a profound way how we perform
molecular simulations. By making it possible to store in a
standardized way not only the input and output of a simulation, but
also many intermediate data items that are usually handled opaquely
inside a simulation program, Mosaic enables the transition from
black-box simulation packages to ecosystems of small programs that
communicate through Mosaic data. This has a number of advantages:

* Small programs are easier to write and easier to understand.
  Individual researchers and small groups will be able to make
  contributions to simulation methodology, without having to develop
  a complete suite of simulation software, or to understand
  someone else's black-box code.

* Intermediate steps that are stored in user-accessible files
  can be inspected and thus verified.

* The core simulation engines, which run Molecular Dynamics and
  similar long-running algorithms, become not only simpler, but also
  more general, serving a much wider community. This leads to
  increased payoffs for optimization and fine-tuning for specific
  architectures. It is quite possible that supercomputer vendors
  will provide an optimized simulation engine for their hardware
  if a single program will cover the needs of biology, material
  science, and other application domains.

* Each small program can be developed using the most appropriate
  programming language and developement tools.


## Visualization

Molecular visualization programs typically load files containing a
molecular configuration associated with some supporting information,
whose details depend on the format being used. Various other
characteristics are often inferred from the explicitly supplied
information, with more or less satisfactory results.

Protein visualization, for example, is based on PDB files, which
provide an atom name and a residue name for each atom, in addition to
its position. The chemical element is inferred from the atom and
residue names, and the bonds are inferred from the same information
plus the atom positions. This inference works reasonably well for
standard residue types. The more a molecular system differs from a
"typical" PDB entry, the more problems appear. Visualisation of
coarse-grained models, for example, is rather frustrating.

Mosaic improves the situation by storing a much more detailed
description of the molecular system that is visualized. Inference of
additional required information is no longer necessary.

Mosaic also makes it possible to visualize additional quantities
related to a molecular system. Quantities like partial charges or
atomic fluctuation amplitudes can be visualized by color scales or
sphere radii. Vector quantities, such as velocities or normal mode
displacements, can be shown as arrows or through animations.


## Analyzing simulations

Programs that analyze the output of molecular simulations
(e.g. Molecular Dynamics trajectories) are currently either written to
work with a specific simulation package, or have to deal with multiple
formats and data conversion issues.  In other words, authors have to
choose between restricted applicability and
[accidental complexity](http://en.wikipedia.org/wiki/Accidental_complexity).
With Mosaic, it becomes possible to write simple and small analysis
programs that nevertheless work with everyone's data.
