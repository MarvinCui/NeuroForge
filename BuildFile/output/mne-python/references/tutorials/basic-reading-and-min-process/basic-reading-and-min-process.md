# How To: Basic Reading And Min Process

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test reading SNIRF files and minimum typical processing.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `datetime`
- `shutil`
- `contextlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne._fiff.constants`
- `mne.datasets.testing`
- `mne.io`
- `mne.io.tests.test_raw`
- `mne.preprocessing.nirs`
- `mne.transforms`
- `mne.utils`
- `shutil`

**Setup Required:**
```python
# Fixtures: fname
```

## Step-by-Step Guide

### Step 1: 'Test reading SNIRF files and minimum typical processing.'

```python
'Test reading SNIRF files and minimum typical processing.'
```

**Verification:**
```python
assert 'hbo' in raw
```

### Step 2: Assign raw = read_raw_snirf(...)

```python
raw = read_raw_snirf(fname, preload=True)
```

**Verification:**
```python
assert 'hbr' in raw
```

### Step 3: Assign raw = optical_density(...)

```python
raw = optical_density(raw)
```

### Step 4: Assign raw = beer_lambert_law(...)

```python
raw = beer_lambert_law(raw, ppf=6)
```


## Complete Example

```python
# Setup
# Fixtures: fname

# Workflow
'Test reading SNIRF files and minimum typical processing.'
raw = read_raw_snirf(fname, preload=True)
if 'fnirs_cw_amplitude' in raw:
    raw = optical_density(raw)
if 'fnirs_od' in raw:
    raw = beer_lambert_law(raw, ppf=6)
assert 'hbo' in raw
assert 'hbr' in raw
```

## Next Steps


---

*Source: test_snirf.py:106 | Complexity: Intermediate | Last updated: 2026-05-18*