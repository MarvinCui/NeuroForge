# How To: Time As Index Ref

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test indexing of raw times.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `math`
- `os`
- `re`
- `contextlib`
- `io`
- `os`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne`
- `mne._fiff._digitization`
- `mne._fiff.constants`
- `mne._fiff.meas_info`
- `mne._fiff.pick`
- `mne._fiff.proj`
- `mne._fiff.utils`
- `mne.io`
- `mne.io.base`
- `mne.transforms`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: offset, origin
```

## Step-by-Step Guide

### Step 1: 'Test indexing of raw times.'

```python
'Test indexing of raw times.'
```

**Verification:**
```python
assert_array_equal(inds, np.arange(raw.n_times))
```

### Step 2: Assign info = create_info(...)

```python
info = create_info(ch_names=10, sfreq=10.0)
```

### Step 3: Assign raw = RawArray(...)

```python
raw = RawArray(data=np.empty((10, 10)), info=info, first_samp=10)
```

### Step 4: Call raw.set_meas_date()

```python
raw.set_meas_date(1)
```

### Step 5: Assign relative_times = value

```python
relative_times = raw.times
```

### Step 6: Assign inds = raw.time_as_index(...)

```python
inds = raw.time_as_index(relative_times + offset, use_rounding=True, origin=origin)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(inds, np.arange(raw.n_times))
```


## Complete Example

```python
# Setup
# Fixtures: offset, origin

# Workflow
'Test indexing of raw times.'
info = create_info(ch_names=10, sfreq=10.0)
raw = RawArray(data=np.empty((10, 10)), info=info, first_samp=10)
raw.set_meas_date(1)
relative_times = raw.times
inds = raw.time_as_index(relative_times + offset, use_rounding=True, origin=origin)
assert_array_equal(inds, np.arange(raw.n_times))
```

## Next Steps


---

*Source: test_raw.py:673 | Complexity: Intermediate | Last updated: 2026-05-18*