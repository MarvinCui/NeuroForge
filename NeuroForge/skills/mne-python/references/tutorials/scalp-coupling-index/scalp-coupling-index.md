# How To: Scalp Coupling Index

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test converting NIRX files.

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
# Fixtures: fname, fmt, tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test converting NIRX files.'

```python
'Test converting NIRX files.'
```

**Verification:**
```python
assert fmt in ('nirx', 'fif')
```

### Step 2: Assign raw = read_raw_nirx(...)

```python
raw = read_raw_nirx(fname)
```

**Verification:**
```python
assert_array_less(sci, 1.0)
```

### Step 3: Assign raw = optical_density(...)

```python
raw = optical_density(raw)
```

**Verification:**
```python
assert_array_less(sci * -1.0, 1.0)
```

### Step 4: Assign sci = scalp_coupling_index(...)

```python
sci = scalp_coupling_index(raw)
```

**Verification:**
```python
assert_allclose(sci[0:6], [1, 1, 1, 1, -1, -1], atol=0.01)
```

### Step 5: Call assert_array_less()

```python
assert_array_less(sci, 1.0)
```

**Verification:**
```python
assert np.abs(sci[6]) < 0.5
```

### Step 6: Call assert_array_less()

```python
assert_array_less(sci * -1.0, 1.0)
```

**Verification:**
```python
assert np.abs(sci[7]) < 0.5
```

### Step 7: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(0)
```

**Verification:**
```python
assert_allclose(sci[8:12], 0, atol=1e-10)
```

### Step 8: Assign new_data = rng.rand(...)

```python
new_data = rng.rand(raw._data[0].shape[0])
```

### Step 9: Assign unknown = new_data

```python
raw._data[0] = new_data
```

### Step 10: Assign unknown = new_data

```python
raw._data[1] = new_data
```

### Step 11: Assign unknown = new_data

```python
raw._data[2] = new_data
```

### Step 12: Assign unknown = value

```python
raw._data[3] = new_data * 0.3
```

### Step 13: Assign unknown = new_data

```python
raw._data[4] = new_data
```

### Step 14: Assign unknown = value

```python
raw._data[5] = new_data * -1.0
```

### Step 15: Assign unknown = new_data

```python
raw._data[6] = new_data
```

### Step 16: Assign unknown = rng.rand(...)

```python
raw._data[7] = rng.rand(raw._data[0].shape[0])
```

### Step 17: Assign unknown = 0.0

```python
raw._data[8] = 0.0
```

### Step 18: Assign unknown = 1.0

```python
raw._data[9] = 1.0
```

### Step 19: Assign unknown = 2.0

```python
raw._data[10] = 2.0
```

### Step 20: Assign unknown = 3.0

```python
raw._data[11] = 3.0
```

### Step 21: Assign sci = scalp_coupling_index(...)

```python
sci = scalp_coupling_index(raw)
```

### Step 22: Call assert_allclose()

```python
assert_allclose(sci[0:6], [1, 1, 1, 1, -1, -1], atol=0.01)
```

**Verification:**
```python
assert np.abs(sci[6]) < 0.5
```

### Step 23: Call assert_allclose()

```python
assert_allclose(sci[8:12], 0, atol=1e-10)
```

### Step 24: Assign raw = beer_lambert_law(...)

```python
raw = beer_lambert_law(raw, ppf=6)
```

### Step 25: Call scalp_coupling_index()

```python
scalp_coupling_index(raw)
```

### Step 26: Call scalp_coupling_index()

```python
scalp_coupling_index(raw)
```


## Complete Example

```python
# Setup
# Fixtures: fname, fmt, tmp_path

# Workflow
'Test converting NIRX files.'
assert fmt in ('nirx', 'fif')
raw = read_raw_nirx(fname)
with pytest.raises(RuntimeError, match='Scalp'):
    scalp_coupling_index(raw)
raw = optical_density(raw)
sci = scalp_coupling_index(raw)
assert_array_less(sci, 1.0)
assert_array_less(sci * -1.0, 1.0)
rng = np.random.RandomState(0)
new_data = rng.rand(raw._data[0].shape[0])
raw._data[0] = new_data
raw._data[1] = new_data
raw._data[2] = new_data
raw._data[3] = new_data * 0.3
raw._data[4] = new_data
raw._data[5] = new_data * -1.0
raw._data[6] = new_data
raw._data[7] = rng.rand(raw._data[0].shape[0])
raw._data[8] = 0.0
raw._data[9] = 1.0
raw._data[10] = 2.0
raw._data[11] = 3.0
sci = scalp_coupling_index(raw)
assert_allclose(sci[0:6], [1, 1, 1, 1, -1, -1], atol=0.01)
assert np.abs(sci[6]) < 0.5
assert np.abs(sci[7]) < 0.5
assert_allclose(sci[8:12], 0, atol=1e-10)
raw = beer_lambert_law(raw, ppf=6)
with pytest.raises(RuntimeError, match='Scalp'):
    scalp_coupling_index(raw)
```

## Next Steps


---

*Source: test_scalp_coupling_index.py:34 | Complexity: Advanced | Last updated: 2026-05-18*