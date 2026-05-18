# How To: Get Data Tmin Tmax

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test tmin and tmax parameters of get_data method.

## Prerequisites

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


## Step-by-Step Guide

### Step 1: 'Test tmin and tmax parameters of get_data method.'

```python
'Test tmin and tmax parameters of get_data method.'
```

**Verification:**
```python
assert_allclose(d1[:, idxs[0]:idxs[1]], d2)
```

### Step 2: Assign fname = value

```python
fname = Path(__file__).parent / 'data' / 'test_raw.fif'
```

**Verification:**
```python
assert_allclose(d3, d1)
```

### Step 3: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(fname)
```

**Verification:**
```python
assert_allclose(d4, d1)
```

### Step 4: Assign unknown = value

```python
tmin, tmax = (1, 9)
```

**Verification:**
```python
assert d5.shape[1] == 1
```

### Step 5: Assign d1 = raw.get_data(...)

```python
d1 = raw.get_data()
```

### Step 6: Assign d2 = raw.get_data(...)

```python
d2 = raw.get_data(tmin=tmin, tmax=tmax)
```

### Step 7: Assign idxs = raw.time_as_index(...)

```python
idxs = raw.time_as_index([tmin, tmax])
```

### Step 8: Call assert_allclose()

```python
assert_allclose(d1[:, idxs[0]:idxs[1]], d2)
```

### Step 9: Assign d3 = raw.get_data(...)

```python
d3 = raw.get_data(tmin=-5)
```

### Step 10: Call assert_allclose()

```python
assert_allclose(d3, d1)
```

### Step 11: Assign d4 = raw.get_data(...)

```python
d4 = raw.get_data(tmax=1000000.0)
```

### Step 12: Call assert_allclose()

```python
assert_allclose(d4, d1)
```

### Step 13: Assign d5 = raw.get_data(...)

```python
d5 = raw.get_data(start=1, stop=2, tmin=tmin, tmax=tmax)
```

**Verification:**
```python
assert d5.shape[1] == 1
```

### Step 14: Call raw.get_data()

```python
raw.get_data(start=None)
```

### Step 15: Call raw.get_data()

```python
raw.get_data(stop=2.3)
```

### Step 16: Call raw.get_data()

```python
raw.get_data(tmin=[1, 2])
```

### Step 17: Call raw.get_data()

```python
raw.get_data(tmax=[1, 2])
```


## Complete Example

```python
# Workflow
'Test tmin and tmax parameters of get_data method.'
fname = Path(__file__).parent / 'data' / 'test_raw.fif'
raw = read_raw_fif(fname)
tmin, tmax = (1, 9)
d1 = raw.get_data()
d2 = raw.get_data(tmin=tmin, tmax=tmax)
idxs = raw.time_as_index([tmin, tmax])
assert_allclose(d1[:, idxs[0]:idxs[1]], d2)
d3 = raw.get_data(tmin=-5)
assert_allclose(d3, d1)
d4 = raw.get_data(tmax=1000000.0)
assert_allclose(d4, d1)
d5 = raw.get_data(start=1, stop=2, tmin=tmin, tmax=tmax)
assert d5.shape[1] == 1
with pytest.raises(TypeError, match='start must be .* int'):
    raw.get_data(start=None)
with pytest.raises(TypeError, match='stop must be .* int'):
    raw.get_data(stop=2.3)
with pytest.raises(TypeError, match='tmin must be .* float'):
    raw.get_data(tmin=[1, 2])
with pytest.raises(TypeError, match='tmax must be .* float'):
    raw.get_data(tmax=[1, 2])
```

## Next Steps


---

*Source: test_raw.py:1022 | Complexity: Advanced | Last updated: 2026-05-18*