# How To: Spectrum Array

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test EpochsSpectrumArray and SpectrumArray constructors.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `datetime`
- `re`
- `functools`
- `numpy`
- `pytest`
- `matplotlib.colors`
- `numpy.testing`
- `mne`
- `mne.channels`
- `mne.io`
- `mne.time_frequency`
- `mne.time_frequency.multitaper`
- `mne.time_frequency.spectrum`
- `mne.utils`
- `pandas.testing`
- `pandas`
- `pandas.testing`
- `mne.utils.dataframe`
- `matplotlib.pyplot`

**Setup Required:**
```python
# Fixtures: kind, method, output, average, tmp_path, request
```

## Step-by-Step Guide

### Step 1: 'Test EpochsSpectrumArray and SpectrumArray constructors.'

```python
'Test EpochsSpectrumArray and SpectrumArray constructors.'
```

### Step 2: Assign dim_names = value

```python
dim_names = ('epoch', 'channel') if kind == 'epochs' else ('channel',)
```

### Step 3: Assign unknown = spectrum.get_data(...)

```python
data, freqs = spectrum.get_data(return_freqs=True)
```

### Step 4: Assign Klass = value

```python
Klass = SpectrumArray if kind == 'raw' else EpochsSpectrumArray
```

### Step 5: Assign spect_arr = Klass(...)

```python
spect_arr = Klass(data=data, info=spectrum.info, freqs=freqs, dim_names=dim_names, weights=spectrum.weights)
```

### Step 6: Call _check_spectrum_equivalent()

```python
_check_spectrum_equivalent(spectrum, spect_arr, tmp_path)
```

### Step 7: Assign spectrum = request.getfixturevalue(...)

```python
spectrum = request.getfixturevalue(f'{kind}_spectrum')
```

### Step 8: Assign data = request.getfixturevalue(...)

```python
data = request.getfixturevalue(kind)
```

### Step 9: Assign kwargs = dict(...)

```python
kwargs = dict()
```

### Step 10: Assign spectrum = data.compute_psd(...)

```python
spectrum = data.compute_psd(method=method, output=output, **kwargs)
```

### Step 11: Call kwargs.update()

```python
kwargs.update(average=average)
```


## Complete Example

```python
# Setup
# Fixtures: kind, method, output, average, tmp_path, request

# Workflow
'Test EpochsSpectrumArray and SpectrumArray constructors.'
dim_names = ('epoch', 'channel') if kind == 'epochs' else ('channel',)
if method == 'welch':
    dim_names += ('freq',) if average else ('freq', 'segment')
else:
    dim_names += ('freq',) if output == 'power' else ('taper', 'freq')
if method == 'welch' and output == 'power' and average:
    spectrum = request.getfixturevalue(f'{kind}_spectrum')
else:
    data = request.getfixturevalue(kind)
    kwargs = dict()
    if method == 'welch':
        kwargs.update(average=average)
    spectrum = data.compute_psd(method=method, output=output, **kwargs)
data, freqs = spectrum.get_data(return_freqs=True)
Klass = SpectrumArray if kind == 'raw' else EpochsSpectrumArray
spect_arr = Klass(data=data, info=spectrum.info, freqs=freqs, dim_names=dim_names, weights=spectrum.weights)
_check_spectrum_equivalent(spectrum, spect_arr, tmp_path)
```

## Next Steps


---

*Source: test_spectrum.py:661 | Complexity: Advanced | Last updated: 2026-05-18*