# How To: Temporal Derivative Distribution Repair

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test running artifact rejection.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne.datasets`
- `mne.datasets.testing`
- `mne.io`
- `mne.preprocessing.nirs`

**Setup Required:**
```python
# Fixtures: fname, tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test running artifact rejection.'

```python
'Test running artifact rejection.'
```

**Verification:**
```python
assert np.max(np.diff(raw_od._data[0])) > shift_amp
```

### Step 2: Assign raw = read_raw_nirx(...)

```python
raw = read_raw_nirx(fname)
```

**Verification:**
```python
assert np.max(np.diff(raw_od._data[0])) < shift_amp
```

### Step 3: Assign raw_od = optical_density(...)

```python
raw_od = optical_density(raw)
```

**Verification:**
```python
assert_allclose(raw_od._data[1], 0.0)
```

### Step 4: Assign raw_hb = beer_lambert_law(...)

```python
raw_hb = beer_lambert_law(raw_od)
```

**Verification:**
```python
assert_allclose(raw_od._data[2], 1.0)
```

### Step 5: Assign max_shift = np.max(...)

```python
max_shift = np.max(np.diff(raw_od._data[0]))
```

**Verification:**
```python
assert np.max(np.diff(raw_hb._data[0])) > shift_amp
```

### Step 6: Assign shift_amp = value

```python
shift_amp = 5 * max_shift
```

**Verification:**
```python
assert np.max(np.diff(raw_hb._data[0])) < shift_amp
```

### Step 7: Assign unknown = value

```python
raw_od._data[0, 0:30] = raw_od._data[0, 0:30] - shift_amp
```

**Verification:**
```python
assert_allclose(raw_hb._data[1], 0.0)
```

### Step 8: Assign unknown = 0.0

```python
raw_od._data[1] = 0.0
```

**Verification:**
```python
assert_allclose(raw_hb._data[2], 1.0)
```

### Step 9: Assign unknown = 1.0

```python
raw_od._data[2] = 1.0
```

**Verification:**
```python
assert np.max(np.diff(raw_od._data[0])) > shift_amp
```

### Step 10: Assign raw_od = tddr(...)

```python
raw_od = tddr(raw_od)
```

**Verification:**
```python
assert np.max(np.diff(raw_od._data[0])) < shift_amp
```

### Step 11: Call assert_allclose()

```python
assert_allclose(raw_od._data[1], 0.0)
```

### Step 12: Call assert_allclose()

```python
assert_allclose(raw_od._data[2], 1.0)
```

### Step 13: Assign max_shift = np.max(...)

```python
max_shift = np.max(np.diff(raw_hb._data[0]))
```

### Step 14: Assign shift_amp = value

```python
shift_amp = 5 * max_shift
```

### Step 15: Assign unknown = value

```python
raw_hb._data[0, 0:30] = raw_hb._data[0, 0:30] - 1.1 * shift_amp
```

### Step 16: Assign unknown = 0.0

```python
raw_hb._data[1] = 0.0
```

### Step 17: Assign unknown = 1.0

```python
raw_hb._data[2] = 1.0
```

**Verification:**
```python
assert np.max(np.diff(raw_hb._data[0])) > shift_amp
```

### Step 18: Assign raw_hb = tddr(...)

```python
raw_hb = tddr(raw_hb)
```

**Verification:**
```python
assert np.max(np.diff(raw_hb._data[0])) < shift_amp
```

### Step 19: Call assert_allclose()

```python
assert_allclose(raw_hb._data[1], 0.0)
```

### Step 20: Call assert_allclose()

```python
assert_allclose(raw_hb._data[2], 1.0)
```


## Complete Example

```python
# Setup
# Fixtures: fname, tmp_path

# Workflow
'Test running artifact rejection.'
raw = read_raw_nirx(fname)
raw_od = optical_density(raw)
raw_hb = beer_lambert_law(raw_od)
max_shift = np.max(np.diff(raw_od._data[0]))
shift_amp = 5 * max_shift
raw_od._data[0, 0:30] = raw_od._data[0, 0:30] - shift_amp
raw_od._data[1] = 0.0
raw_od._data[2] = 1.0
assert np.max(np.diff(raw_od._data[0])) > shift_amp
raw_od = tddr(raw_od)
assert np.max(np.diff(raw_od._data[0])) < shift_amp
assert_allclose(raw_od._data[1], 0.0)
assert_allclose(raw_od._data[2], 1.0)
max_shift = np.max(np.diff(raw_hb._data[0]))
shift_amp = 5 * max_shift
raw_hb._data[0, 0:30] = raw_hb._data[0, 0:30] - 1.1 * shift_amp
raw_hb._data[1] = 0.0
raw_hb._data[2] = 1.0
assert np.max(np.diff(raw_hb._data[0])) > shift_amp
raw_hb = tddr(raw_hb)
assert np.max(np.diff(raw_hb._data[0])) < shift_amp
assert_allclose(raw_hb._data[1], 0.0)
assert_allclose(raw_hb._data[2], 1.0)
```

## Next Steps


---

*Source: test_temporal_derivative_distribution_repair.py:21 | Complexity: Advanced | Last updated: 2026-05-18*