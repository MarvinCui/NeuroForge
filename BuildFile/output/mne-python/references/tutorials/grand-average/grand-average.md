# How To: Grand Average

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test `grand_average()` works for instances of `BaseSpectrum`.

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
# Fixtures: raw_spectrum
```

## Step-by-Step Guide

### Step 1: 'Test `grand_average()` works for instances of `BaseSpectrum`.'

```python
'Test `grand_average()` works for instances of `BaseSpectrum`.'
```

**Verification:**
```python
assert_allclose(new_spectrum.data, spectrum1.data * 1.5)
```

### Step 2: Assign spectrum1 = raw_spectrum.copy(...)

```python
spectrum1 = raw_spectrum.copy()
```

### Step 3: Assign spectrum2 = raw_spectrum.copy(...)

```python
spectrum2 = raw_spectrum.copy()
```

### Step 4: Assign new_spectrum = grand_average(...)

```python
new_spectrum = grand_average([spectrum1, spectrum2])
```

### Step 5: Call assert_allclose()

```python
assert_allclose(new_spectrum.data, spectrum1.data * 1.5)
```


## Complete Example

```python
# Setup
# Fixtures: raw_spectrum

# Workflow
'Test `grand_average()` works for instances of `BaseSpectrum`.'
spectrum1 = raw_spectrum.copy()
spectrum2 = raw_spectrum.copy()
spectrum2._data *= 2
new_spectrum = grand_average([spectrum1, spectrum2])
assert_allclose(new_spectrum.data, spectrum1.data * 1.5)
```

## Next Steps


---

*Source: test_spectrum.py:274 | Complexity: Intermediate | Last updated: 2026-05-18*