---
title: MakeGridPoint()
keywords: spherical harmonics software package, spherical harmonic transform, legendre functions, multitaper spectral analysis, fortran, Python, gravity, magnetic field
sidebar: mydoc_sidebar
permalink: pymakegridpoint.html
summary:
tags: [python]
toc: false
editdoc: pydoc
---

Evaluate a real function expressed in real spherical harmonics at a single point.

## Usage

```python
`value` = MakeGridPoint (`cilm`, `lat`, `lon`, [`lmax`, `norm`, `csphase`, `dealloc`])
```

## Returns

`value` : float
:   Value of the function at (`lat`, `lon`).

## Parameters

`cilm` : float, dimension (2, `lmaxin`+1, `lmaxin`+1)
:   The real spherical harmonic coefficients of the function. The coefficients `C0lm` and `C1lm` refer to the cosine (`Clm`) and sine (`Slm`) coefficients, respectively, with `Clm=cilm[0,1,m]` and `Slm=cilm[1,l,m]`.

`lat` : float
:   The latitude of the point in DEGREES.

`lon` : float 
:   The longitude of the point in DEGREES.

`lmax` : optional, integer, default = `lmaxin`
:   The maximum spherical harmonic degree used in evaluating the function.

`norm` : optional, integer, default = 1
:   1 (default) = Geodesy 4-pi normalized harmonics; 2 = Schmidt semi-normalized harmonics; 3 = unnormalized harmonics; 4 = orthonormal harmonics.

`csphase` : optional, integer, default = 1
:   1 (default) = do not apply the Condon-Shortley phase factor to the associated Legendre functions; -1 = append the Condon-Shortley phase factor of (-1)^m to the associated Legendre functions.

`dealloc` : optional, integer, default = 0
:   0 (default) = Save variables used in the external Legendre function calls. (1) Deallocate this memory at the end of the funcion call.

## Description

`MakeGridPoint` will expand a function expressed in spherical harmonics at a single point. The input latitude and longitude are in degrees, and the maximum degree used in evaluating the function is the smaller of `lmaxin` and `lmax`. The employed spherical harmonic normalization and Condon-Shortley phase convention can be set by the optional arguments `norm` and `csphase`; if not set, the default is to use geodesy 4-pi normalized harmonics that exclude the Condon-Shortley phase of (-1)^m.
