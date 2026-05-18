# How To: Array Copy

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test copying during construction.

## Prerequisites

**Required Modules:**
- `pathlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.meas_info`
- `mne._fiff.pick`
- `mne.channels`
- `mne.io`
- `mne.io.array`
- `mne.io.tests.test_raw`


## Step-by-Step Guide

### Step 1: 'Test copying during construction.'

```python
'Test copying during construction.'
```

**Verification:**
```python
assert raw._data is data
```

### Step 2: Assign info = create_info(...)

```python
info = create_info(1, 1000.0)
```

**Verification:**
```python
assert raw.info is not info
```

### Step 3: Assign data = np.zeros(...)

```python
data = np.zeros((1, 1000))
```

**Verification:**
```python
assert raw._data is not data
```

### Step 4: Assign raw = RawArray(...)

```python
raw = RawArray(data, info)
```

**Verification:**
```python
assert raw.info is not info
```

### Step 5: Assign raw = RawArray(...)

```python
raw = RawArray(data.astype(np.float32), info)
```

**Verification:**
```python
assert raw._data is data
```

### Step 6: Assign raw = RawArray(...)

```python
raw = RawArray(data, info, copy='info')
```

**Verification:**
```python
assert raw.info is not info
```

### Step 7: Assign raw = RawArray(...)

```python
raw = RawArray(data, info, copy='data')
```

**Verification:**
```python
assert raw._data is not data
```

### Step 8: Assign raw = RawArray(...)

```python
raw = RawArray(data, info, copy='both')
```

**Verification:**
```python
assert raw.info is info
```

### Step 9: Assign raw = RawArray(...)

```python
raw = RawArray(data.astype(np.float32), info, copy='both')
```

**Verification:**
```python
assert raw._data is not data
```

### Step 10: Assign raw = RawArray(...)

```python
raw = RawArray(data, info, copy=None)
```

**Verification:**
```python
assert raw.info is not info
```

### Step 11: Call RawArray()

```python
RawArray(data.astype(np.float32), info, copy='info')
```

**Verification:**
```python
assert raw._data is not data
```

### Step 12: Call RawArray()

```python
RawArray(data.astype(np.float32), info, copy=None)
```

**Verification:**
```python
assert raw.info is not info
```


## Complete Example

```python
# Workflow
'Test copying during construction.'
info = create_info(1, 1000.0)
data = np.zeros((1, 1000))
raw = RawArray(data, info)
assert raw._data is data
assert raw.info is not info
raw = RawArray(data.astype(np.float32), info)
assert raw._data is not data
assert raw.info is not info
raw = RawArray(data, info, copy='info')
assert raw._data is data
assert raw.info is not info
with pytest.raises(ValueError, match="data copying was not .* copy='info"):
    RawArray(data.astype(np.float32), info, copy='info')
raw = RawArray(data, info, copy='data')
assert raw._data is not data
assert raw.info is info
raw = RawArray(data, info, copy='both')
assert raw._data is not data
assert raw.info is not info
raw = RawArray(data.astype(np.float32), info, copy='both')
assert raw._data is not data
assert raw.info is not info
raw = RawArray(data, info, copy=None)
assert raw._data is data
assert raw.info is info
with pytest.raises(ValueError, match='data copying was not .* copy=None'):
    RawArray(data.astype(np.float32), info, copy=None)
```

## Next Steps


---

*Source: test_array.py:41 | Complexity: Advanced | Last updated: 2026-05-18*