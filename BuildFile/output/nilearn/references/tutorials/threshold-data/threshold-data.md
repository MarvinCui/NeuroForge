# How To: Threshold Data

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test threshold data

## Prerequisites

**Required Modules:**
- `base64`
- `io`
- `numpy`
- `pytest`
- `matplotlib`
- `nibabel`
- `nilearn`
- `nilearn.conftest`
- `nilearn.image`
- `nilearn.plotting._engine_utils`
- `nilearn.plotting.html_stat_map`


## Step-by-Step Guide

### Step 1: Assign data = np.arange(...)

```python
data = np.arange(-3, 4)
```

**Verification:**
```python
assert (mask == gtruth_m).all()
```

### Step 2: Assign unknown = _threshold_data(...)

```python
data_t, mask, _ = _threshold_data(data, threshold='auto')
```

**Verification:**
```python
assert (data_t == gtruth_d).all()
```

### Step 3: Assign gtruth_m = np.array(...)

```python
gtruth_m = np.array([False, True, True, True, True, True, False])
```

**Verification:**
```python
assert np.all(np.logical_not(mask))
```

### Step 4: Assign gtruth_d = np.array(...)

```python
gtruth_d = np.array([-3, 0, 0, 0, 0, 0, 3])
```

**Verification:**
```python
assert np.all(data_t == data)
```

### Step 5: Assign unknown = _threshold_data(...)

```python
data_t, mask, _ = _threshold_data(data, threshold=None)
```

**Verification:**
```python
assert (mask == gtruth).all()
```

### Step 6: Assign unknown = _threshold_data(...)

```python
data_t, mask, _ = _threshold_data(data, threshold=1)
```

**Verification:**
```python
assert (mask == gtruth).all()
```

### Step 7: Assign gtruth = np.array(...)

```python
gtruth = np.array([False, False, True, True, True, False, False])
```

**Verification:**
```python
assert (mask == gtruth).all()
```

### Step 8: Assign unknown = _threshold_data(...)

```python
data_t, mask, _ = _threshold_data(data, threshold=0)
```

### Step 9: Assign gtruth = np.array(...)

```python
gtruth = np.array([False, False, False, True, False, False, False])
```

**Verification:**
```python
assert (mask == gtruth).all()
```

### Step 10: Assign data = np.arange(...)

```python
data = np.arange(3, 10)
```

### Step 11: Assign unknown = _threshold_data(...)

```python
data_t, mask, _ = _threshold_data(data, threshold=2)
```

### Step 12: Assign gtruth = np.full(...)

```python
gtruth = np.full(7, False)
```

**Verification:**
```python
assert (mask == gtruth).all()
```


## Complete Example

```python
# Workflow
data = np.arange(-3, 4)
data_t, mask, _ = _threshold_data(data, threshold='auto')
gtruth_m = np.array([False, True, True, True, True, True, False])
gtruth_d = np.array([-3, 0, 0, 0, 0, 0, 3])
assert (mask == gtruth_m).all()
assert (data_t == gtruth_d).all()
data_t, mask, _ = _threshold_data(data, threshold=None)
assert np.all(np.logical_not(mask))
assert np.all(data_t == data)
data_t, mask, _ = _threshold_data(data, threshold=1)
gtruth = np.array([False, False, True, True, True, False, False])
assert (mask == gtruth).all()
data_t, mask, _ = _threshold_data(data, threshold=0)
gtruth = np.array([False, False, False, True, False, False, False])
assert (mask == gtruth).all()
data = np.arange(3, 10)
data_t, mask, _ = _threshold_data(data, threshold=2)
gtruth = np.full(7, False)
assert (mask == gtruth).all()
```

## Next Steps


---

*Source: test_html_stat_map.py:97 | Complexity: Advanced | Last updated: 2026-05-18*