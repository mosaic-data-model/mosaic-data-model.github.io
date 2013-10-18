---
layout: default
title: Design criteria
---

# MOSAIC design criteria

## Completeness

Ideally, Mosaic should be able to handle any data whatsoever that is
related to molecular simulations. Since no exhaustive list could ever
be written down, this requires a modular and extensible design.

Completeness also implies that a Mosaic data file should be as
autonomous as possible. All its contents should ideally be
interpretable without reference to external data sources.

The completeness criterion is motivated by the principles of
[Reproducible Research](http://en.wikipedia.org/wiki/Reproducibility).
Reliance on unpublished data, or data in incompletely
documented formats, is one of the major causes of non-reproducibility.

## Machine independence

Mosaic data files should be readable on any computing platform, present
and future. This requires that all file formats must be specified
unamiguously down to the byte level.

## Efficiency

Mosaic must be able to handle big data sets (a few GB are not
untypical nowadays), which requires compact storage and fast I/O. This
aspect is currently covered by the HDF5 implementation of Mosaic.

## As few software dependencies as possible

Scientific data has a longer lifetime than most scientific software.
The interpretation of Mosaic data should not depend on a complex
software stack that may become unusable because of lack of
maintenance. It should also be possible to handle Mosaic data in any
programming language, current or future, without the requirement to be
able to link to any specific other programming language.

This goal is fully achieved with the XML implementation. The HDF5
implementation depends *de facto* on the HDF5 library, although the
file format is documented and partial alternative implementations
exist. The Mosaic code library itself is proposed as a convenience,
but not required.

