# How To: Crop Append

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test crop and append raw.

## Prerequisites

**Required Modules:**
- `os`
- `collections`
- `functools`
- `io`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne`
- `mne._fiff._digitization`
- `mne._fiff.constants`
- `mne.datasets`
- `mne.io`
- `mne.io.bti.bti`
- `mne.io.tests.test_raw`
- `mne.transforms`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test crop and append raw.'

```python
'Test crop and append raw.'
```

**Verification:**
```python
assert y_.shape[1] == mask.sum()
```

### Step 2: Assign raw = _test_raw_reader(...)

```python
raw = _test_raw_reader(read_raw_bti, pdf_fname=pdf_fnames[0], config_fname=config_fnames[0], head_shape_fname=hs_fnames[0])
```

**Verification:**
```python
assert y_.shape[0] == y.shape[0]
```

### Step 3: Assign unknown = value

```python
y, t = raw[:]
```

### Step 4: Assign unknown = value

```python
t0, t1 = (0.25 * t[-1], 0.75 * t[-1])
```

### Step 5: Assign mask = value

```python
mask = (t0 <= t) * (t <= t1)
```

### Step 6: Assign raw_ = raw.copy.crop(...)

```python
raw_ = raw.copy().crop(t0, t1)
```

### Step 7: Assign unknown = value

```python
y_, _ = raw_[:]
```

**Verification:**
```python
assert y_.shape[1] == mask.sum()
```


## Complete Example

```python
# Workflow
'Test crop and append raw.'
raw = _test_raw_reader(read_raw_bti, pdf_fname=pdf_fnames[0], config_fname=config_fnames[0], head_shape_fname=hs_fnames[0])
y, t = raw[:]
t0, t1 = (0.25 * t[-1], 0.75 * t[-1])
mask = (t0 <= t) * (t <= t1)
raw_ = raw.copy().crop(t0, t1)
y_, _ = raw_[:]
assert y_.shape[1] == mask.sum()
assert y_.shape[0] == y.shape[0]
```

## Next Steps


---

*Source: test_bti.py:102 | Complexity: Intermediate | Last updated: 2026-05-18*