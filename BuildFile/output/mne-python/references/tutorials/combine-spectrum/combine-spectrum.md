# How To: Combine Spectrum

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test `combine_spectrum()` works.

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
# Fixtures: raw_spectrum, weights
```

## Step-by-Step Guide

### Step 1: 'Test `combine_spectrum()` works.'

```python
'Test `combine_spectrum()` works.'
```

**Verification:**
```python
assert_allclose(new_spectrum.data, spectrum1.data * (5 / 3))
```

### Step 2: Assign spectrum1 = raw_spectrum.copy(...)

```python
spectrum1 = raw_spectrum.copy()
```

**Verification:**
```python
assert_allclose(new_spectrum.data, spectrum1.data * 1.5)
```

### Step 3: Assign spectrum2 = raw_spectrum.copy(...)

```python
spectrum2 = raw_spectrum.copy()
```

**Verification:**
```python
assert_allclose(new_spectrum.data, 0)
```

### Step 4: Assign spectrum1.nave = 1

```python
spectrum1.nave = 1
```

### Step 5: Assign spectrum2.nave = 2

```python
spectrum2.nave = 2
```

### Step 6: Assign new_spectrum = combine_spectrum(...)

```python
new_spectrum = combine_spectrum([spectrum1, spectrum2], weights=weights)
```

### Step 7: Call assert_allclose()

```python
assert_allclose(new_spectrum.data, spectrum1.data * (5 / 3))
```

### Step 8: Assign new_spectrum = combine_spectrum(...)

```python
new_spectrum = combine_spectrum([spectrum1, spectrum2], weights=weights)
```

### Step 9: Call assert_allclose()

```python
assert_allclose(new_spectrum.data, spectrum1.data * 1.5)
```

### Step 10: Assign new_spectrum = combine_spectrum(...)

```python
new_spectrum = combine_spectrum([spectrum1, spectrum2], weights=weights)
```

### Step 11: Call assert_allclose()

```python
assert_allclose(new_spectrum.data, 0)
```


## Complete Example

```python
# Setup
# Fixtures: raw_spectrum, weights

# Workflow
'Test `combine_spectrum()` works.'
spectrum1 = raw_spectrum.copy()
spectrum2 = raw_spectrum.copy()
if weights == 'nave':
    spectrum1.nave = 1
    spectrum2.nave = 2
    spectrum2._data *= 2
    new_spectrum = combine_spectrum([spectrum1, spectrum2], weights=weights)
    assert_allclose(new_spectrum.data, spectrum1.data * (5 / 3))
elif weights == 'equal':
    spectrum2._data *= 2
    new_spectrum = combine_spectrum([spectrum1, spectrum2], weights=weights)
    assert_allclose(new_spectrum.data, spectrum1.data * 1.5)
else:
    new_spectrum = combine_spectrum([spectrum1, spectrum2], weights=weights)
    assert_allclose(new_spectrum.data, 0)
```

## Next Steps


---

*Source: test_spectrum.py:226 | Complexity: Advanced | Last updated: 2026-05-18*