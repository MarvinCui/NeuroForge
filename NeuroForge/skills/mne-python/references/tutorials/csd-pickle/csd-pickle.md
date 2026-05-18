# How To: Csd Pickle

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test pickling and unpickling a CrossSpectralDensity.

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test pickling and unpickling a CrossSpectralDensity.'

```python
'Test pickling and unpickling a CrossSpectralDensity.'
```

**Verification:**
```python
assert_array_equal(csd._data, csd2._data)
```

### Step 2: Assign csd = _make_csd(...)

```python
csd = _make_csd()
```

**Verification:**
```python
assert csd.tmin == csd2.tmin
```

### Step 3: Assign tempdir = str(...)

```python
tempdir = str(tmp_path)
```

**Verification:**
```python
assert csd.tmax == csd2.tmax
```

### Step 4: Assign fname = op.join(...)

```python
fname = op.join(tempdir, 'csd.dat')
```

**Verification:**
```python
assert csd.ch_names == csd2.ch_names
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal(csd._data, csd2._data)
```

**Verification:**
```python
assert csd.frequencies == csd2.frequencies
```

### Step 6: Call pickle.dump()

```python
pickle.dump(csd, f)
```

**Verification:**
```python
assert csd._is_sum == csd2._is_sum
```

### Step 7: Assign csd2 = pickle.load(...)

```python
csd2 = pickle.load(f)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test pickling and unpickling a CrossSpectralDensity.'
csd = _make_csd()
tempdir = str(tmp_path)
fname = op.join(tempdir, 'csd.dat')
with open(fname, 'wb') as f:
    pickle.dump(csd, f)
with open(fname, 'rb') as f:
    csd2 = pickle.load(f)
assert_array_equal(csd._data, csd2._data)
assert csd.tmin == csd2.tmin
assert csd.tmax == csd2.tmax
assert csd.ch_names == csd2.ch_names
assert csd.frequencies == csd2.frequencies
assert csd._is_sum == csd2._is_sum
```

## Next Steps


---

*Source: test_csd.py:264 | Complexity: Intermediate | Last updated: 2026-05-18*