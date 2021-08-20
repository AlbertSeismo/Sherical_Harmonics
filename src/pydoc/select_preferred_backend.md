# select_preferred_backend()

Select the preferred backend module used for the spherical harmonic
transforms in pyshtools.

# Usage

```python
select_preferred_backend_module([backend, nthreads])
```

# Parameters

**backend : str, optional, default = 'shtools'**
:   Name of the preferred backend, either 'shtools' or 'ducc'.

**nthreads : int, optional, default = 1**
:   Number of threads to use for the 'ducc' backend. Setting this parameter
        to 0 will use as many threads as there are hardware threads on the
        system.
    