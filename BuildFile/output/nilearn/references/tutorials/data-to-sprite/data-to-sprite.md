# How To: Data To Sprite

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test data to sprite

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

### Step 1: Assign data = np.zeros(...)

```python
data = np.zeros([8, 8, 8])
```

**Verification:**
```python
assert sprite.shape == gtruth.shape, 'shape of sprite not as expected'
```

### Step 2: Assign unknown = 1

```python
data[2:6, 2:6, 2:6] = 1
```

**Verification:**
```python
assert (sprite == gtruth).all(), 'simulated sprite not as expected'
```

### Step 3: Assign sprite = _data_to_sprite(...)

```python
sprite = _data_to_sprite(data)
```

### Step 4: Assign Z = np.zeros(...)

```python
Z = np.zeros([8, 8])
```

### Step 5: Assign Zr = np.zeros(...)

```python
Zr = np.zeros([2, 8])
```

### Step 6: Assign Cr = np.tile(...)

```python
Cr = np.tile(np.array([[0, 0, 1, 1, 1, 1, 0, 0]]), [4, 1])
```

### Step 7: Assign C = np.concatenate(...)

```python
C = np.concatenate((Zr, Cr, Zr), axis=0)
```

### Step 8: Assign gtruth = np.concatenate(...)

```python
gtruth = np.concatenate((np.concatenate((Z, Z, C), axis=1), np.concatenate((C, C, C), axis=1), np.concatenate((Z, Z, Z), axis=1)), axis=0)
```

**Verification:**
```python
assert sprite.shape == gtruth.shape, 'shape of sprite not as expected'
```


## Complete Example

```python
# Workflow
data = np.zeros([8, 8, 8])
data[2:6, 2:6, 2:6] = 1
sprite = _data_to_sprite(data)
Z = np.zeros([8, 8])
Zr = np.zeros([2, 8])
Cr = np.tile(np.array([[0, 0, 1, 1, 1, 1, 0, 0]]), [4, 1])
C = np.concatenate((Zr, Cr, Zr), axis=0)
gtruth = np.concatenate((np.concatenate((Z, Z, C), axis=1), np.concatenate((C, C, C), axis=1), np.concatenate((Z, Z, Z), axis=1)), axis=0)
assert sprite.shape == gtruth.shape, 'shape of sprite not as expected'
assert (sprite == gtruth).all(), 'simulated sprite not as expected'
```

## Next Steps


---

*Source: test_html_stat_map.py:73 | Complexity: Advanced | Last updated: 2026-05-18*