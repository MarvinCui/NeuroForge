# How To: Csd Repr

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test string representation of CrossSpectralDensity.

## Prerequisites

**Required Modules:**
- `pickle`
- `itertools`
- `os`
- `numpy`
- `pytest`
- `numpy.testing`
- `pytest`
- `mne`
- `mne.channels`
- `mne.proj`
- `mne.time_frequency`
- `mne.time_frequency.csd`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test string representation of CrossSpectralDensity.'

```python
'Test string representation of CrossSpectralDensity.'
```

**Verification:**
```python
assert str(csd) == '<CrossSpectralDensity | n_channels=3, time=0.0 to 1.0 s, frequencies=1.0, 2.0, 3.0, 4.0 Hz.>'
```

### Step 2: Assign csd = _make_csd(...)

```python
csd = _make_csd()
```

**Verification:**
```python
assert str(csd.mean()) == '<CrossSpectralDensity | n_channels=3, time=0.0 to 1.0 s, frequencies=1.0-4.0 Hz.>'
```

### Step 3: Assign csd_binned = csd.mean(...)

```python
csd_binned = csd.mean(fmin=[1, 3], fmax=[2, 4])
```

**Verification:**
```python
assert str(csd_binned) == '<CrossSpectralDensity | n_channels=3, time=0.0 to 1.0 s, frequencies=1.0-2.0, 3.0-4.0 Hz.>'
```

### Step 4: Assign csd_binned = csd.mean(...)

```python
csd_binned = csd.mean(fmin=[1, 2], fmax=[1, 4])
```

**Verification:**
```python
assert str(csd_binned) == '<CrossSpectralDensity | n_channels=3, time=0.0 to 1.0 s, frequencies=1.0, 2.0-4.0 Hz.>'
```

### Step 5: Assign csd_no_time = csd.copy(...)

```python
csd_no_time = csd.copy()
```

**Verification:**
```python
assert str(csd_no_time) == '<CrossSpectralDensity | n_channels=3, time=unknown, frequencies=1.0, 2.0, 3.0, 4.0 Hz.>'
```

### Step 6: Assign csd_no_time.tmin = None

```python
csd_no_time.tmin = None
```

### Step 7: Assign csd_no_time.tmax = None

```python
csd_no_time.tmax = None
```

**Verification:**
```python
assert str(csd_no_time) == '<CrossSpectralDensity | n_channels=3, time=unknown, frequencies=1.0, 2.0, 3.0, 4.0 Hz.>'
```


## Complete Example

```python
# Workflow
'Test string representation of CrossSpectralDensity.'
csd = _make_csd()
assert str(csd) == '<CrossSpectralDensity | n_channels=3, time=0.0 to 1.0 s, frequencies=1.0, 2.0, 3.0, 4.0 Hz.>'
assert str(csd.mean()) == '<CrossSpectralDensity | n_channels=3, time=0.0 to 1.0 s, frequencies=1.0-4.0 Hz.>'
csd_binned = csd.mean(fmin=[1, 3], fmax=[2, 4])
assert str(csd_binned) == '<CrossSpectralDensity | n_channels=3, time=0.0 to 1.0 s, frequencies=1.0-2.0, 3.0-4.0 Hz.>'
csd_binned = csd.mean(fmin=[1, 2], fmax=[1, 4])
assert str(csd_binned) == '<CrossSpectralDensity | n_channels=3, time=0.0 to 1.0 s, frequencies=1.0, 2.0-4.0 Hz.>'
csd_no_time = csd.copy()
csd_no_time.tmin = None
csd_no_time.tmax = None
assert str(csd_no_time) == '<CrossSpectralDensity | n_channels=3, time=unknown, frequencies=1.0, 2.0, 3.0, 4.0 Hz.>'
```

## Next Steps


---

*Source: test_csd.py:108 | Complexity: Intermediate | Last updated: 2026-05-18*