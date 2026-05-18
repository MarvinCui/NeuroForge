# How To: Nirsport V1 W Bad Sat

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test NIRSport1 file with NaNs.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `datetime`
- `os`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.datasets.testing`
- `mne.io`
- `mne.io.tests.test_raw`
- `mne.preprocessing`
- `mne.preprocessing.nirs`
- `mne.transforms`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: preload, meas_date
```

## Step-by-Step Guide

### Step 1: 'Test NIRSport1 file with NaNs.'

```python
'Test NIRSport1 file with NaNs.'
```

**Verification:**
```python
assert not np.isnan(data).any()
```

### Step 2: Assign fname = nirsport1_w_fullsat

```python
fname = nirsport1_w_fullsat
```

**Verification:**
```python
assert len(raw.annotations) == 5
```

### Step 3: Assign raw = read_raw_nirx(...)

```python
raw = read_raw_nirx(fname, preload=preload)
```

**Verification:**
```python
assert_allclose(raw_ignore.get_data(), data)
```

### Step 4: Assign data = raw.get_data(...)

```python
data = raw.get_data()
```

**Verification:**
```python
assert len(raw_ignore.annotations) == 2
```

### Step 5: Assign raw_ignore = read_raw_nirx(...)

```python
raw_ignore = read_raw_nirx(fname, saturated='ignore', preload=preload)
```

**Verification:**
```python
assert not any(('NAN' in d for d in raw_ignore.annotations.description))
```

### Step 6: Call assert_allclose()

```python
assert_allclose(raw_ignore.get_data(), data)
```

**Verification:**
```python
assert np.isnan(data_nan).any()
```

### Step 7: Assign raw_nan = read_raw_nirx(...)

```python
raw_nan = read_raw_nirx(fname, saturated='nan', preload=preload)
```

**Verification:**
```python
assert not np.allclose(raw_nan.get_data(), data)
```

### Step 8: Assign data_nan = raw_nan.get_data(...)

```python
data_nan = raw_nan.get_data()
```

**Verification:**
```python
assert nan_annots.orig_time == raw_nan.info['meas_date']
```

### Step 9: Assign raw_nan_annot = raw_ignore.copy(...)

```python
raw_nan_annot = raw_ignore.copy()
```

**Verification:**
```python
assert_allclose(a, b)
```

### Step 10: Assign nan_annots = annotate_nan(...)

```python
nan_annots = annotate_nan(raw_nan)
```

**Verification:**
```python
assert nan_annots.orig_time == raw_nan.info['meas_date']
```

### Step 11: Call raw_nan_annot.set_annotations()

```python
raw_nan_annot.set_annotations(nan_annots)
```

### Step 12: Assign use_mask = np.where(...)

```python
use_mask = np.where(raw.annotations.description == 'BAD_SATURATED')
```

### Step 13: Call raw.set_meas_date()

```python
raw.set_meas_date(None)
```

### Step 14: Call raw_nan.set_meas_date()

```python
raw_nan.set_meas_date(None)
```

### Step 15: Call raw_nan_annot.set_meas_date()

```python
raw_nan_annot.set_meas_date(None)
```

### Step 16: Assign a = value

```python
a = getattr(raw_nan_annot.annotations, key)[::2]
```

### Step 17: Assign b = value

```python
b = getattr(raw.annotations, key)[use_mask]
```

### Step 18: Call assert_allclose()

```python
assert_allclose(a, b)
```


## Complete Example

```python
# Setup
# Fixtures: preload, meas_date

# Workflow
'Test NIRSport1 file with NaNs.'
fname = nirsport1_w_fullsat
raw = read_raw_nirx(fname, preload=preload)
data = raw.get_data()
assert not np.isnan(data).any()
assert len(raw.annotations) == 5
raw_ignore = read_raw_nirx(fname, saturated='ignore', preload=preload)
assert_allclose(raw_ignore.get_data(), data)
assert len(raw_ignore.annotations) == 2
assert not any(('NAN' in d for d in raw_ignore.annotations.description))
raw_nan = read_raw_nirx(fname, saturated='nan', preload=preload)
data_nan = raw_nan.get_data()
assert np.isnan(data_nan).any()
assert not np.allclose(raw_nan.get_data(), data)
raw_nan_annot = raw_ignore.copy()
if meas_date is None:
    raw.set_meas_date(None)
    raw_nan.set_meas_date(None)
    raw_nan_annot.set_meas_date(None)
nan_annots = annotate_nan(raw_nan)
assert nan_annots.orig_time == raw_nan.info['meas_date']
raw_nan_annot.set_annotations(nan_annots)
use_mask = np.where(raw.annotations.description == 'BAD_SATURATED')
for key in ('onset', 'duration'):
    a = getattr(raw_nan_annot.annotations, key)[::2]
    b = getattr(raw.annotations, key)[use_mask]
    assert_allclose(a, b)
```

## Next Steps


---

*Source: test_nirx.py:196 | Complexity: Advanced | Last updated: 2026-05-18*