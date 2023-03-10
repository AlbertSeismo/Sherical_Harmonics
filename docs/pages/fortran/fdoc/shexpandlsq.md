---
title: SHExpandLSQ (Fortran)
keywords: spherical harmonics software package, spherical harmonic transform, legendre functions, multitaper spectral analysis, fortran, Python, gravity, magnetic field
sidebar: fortran_sidebar
permalink: shexpandlsq.html
summary:
tags: [fortran]
toc: false
editdoc: fdoc
---

Expand a set of irregularly sampled data points into spherical harmonics using a (weighted) least squares inversion.

## Usage

call SHExpandLSQ (`cilm`, `d`, `lat`, `lon`, `nmax`, `lmax`, `norm`, `chi2`, `csphase`, `weights`, `exitstatus`)

## Parameters

`cilm` : output, real(dp), dimension (2, `lmax`+1, `lmax`+1)
:   The real spherical harmonic coefficients of the function. The coefficients `C1lm` and `C2lm` refer to the cosine (`Clm`) and sine (`Slm`) coefficients, respectively, with `Clm=cilm(1,l+1,m+1)` and `Slm=cilm(2,l+1,m+1)`.

`d` : input, real(dp), dimension (`nmax`)
:   The value of the function at the coordinates (`lat`, `lon`).

`lat` : input, real(dp), dimension (`nmax`)
:   The latitude in DEGREES corresponding to the value in `d`.

`lon` : input, real(dp), dimension (`nmax`)
:   The longitude in DEGREES corresponding to the value in `d`.

`nmax` : input, integer
:   The number of data points.

`lmax` : input, integer
:   The maximum spherical harmonic degree of the output coefficients `cilm`.

`norm` : input, optional, integer, default = 1
:   1 (default) = Geodesy 4-pi normalized harmonics; 2 = Schmidt semi-normalized harmonics; 3 = unnormalized harmonics; 4 = orthonormal harmonics.

`chi2` : output, optional, real(dp)
:   The residual sum of squares misfit for an overdetermined inversion.

`csphase` : input, optional, integer, default = 1
:   1 (default) = do not apply the Condon-Shortley phase factor to the associated Legendre functions; -1 = append the Condon-Shortley phase factor of (-1)^m to the associated Legendre functions.

`weights` : input, real(dp), dimension (`nmax`)
:   The weights to be applied in a weighted least squares inversion.

`exitstatus` : output, optional, integer
:   If present, instead of executing a STOP when an error is encountered, the variable exitstatus will be returned describing the error. 0 = No errors; 1 = Improper dimensions of input array; 2 = Improper bounds for input variable; 3 = Error allocating memory; 4 = File IO error.

## Description

`SHExpandLSQ` will expand a set of irregularly sampled data points into spherical harmonics by a least squares inversion. When the number of data points is greater or equal to the number of spherical harmonic coefficients (i.e., `nmax>=(lmax+1)**2`), the solution of the overdetermined system will be determined. If there are more coefficients than data points, then the solution of the underdetermined system that minimizes the solution norm will be determined. The inversions are performed using the LAPACK routine DGELS.

A weighted least squares inversion will be performed if the optional vector
`weights` is specified. In this case, the problem must be overdetermined, and it is assumed that each measurement is statistically independent (i.e., the weighting matrix is diagonal). The inversion is performed using the LAPACK routine DGGGLM.

The employed spherical harmonic normalization and Condon-Shortley phase convention can be set by the optional arguments `norm` and `csphase`; if not set, the default is to use geodesy 4-pi normalized harmonics that exclude the Condon-Shortley phase of (-1)^m.

## See also

[makegriddh](makegriddh.html), [shexpanddh](shexpanddh.html), [makegriddhc](makegriddhc.html), [shexpanddhc](shexpanddhc.html), [makegridglq](makegridglq.html), [shexpandglq](shexpandglq.html), [makegridglqc](makegridglqc.html), [shexpandglqc](shexpandglqc.html), dgels(1), dggglm(1)
