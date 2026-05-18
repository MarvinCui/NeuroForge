# How To: Per Array Dict Creation

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test per array dict creation

## Prerequisites

**Required Modules:**
- `copy`
- `operator`
- `unittest`
- `warnings`
- `collections`
- `numpy`
- `pytest`
- `numpy.testing`
- `testing`
- `tractogram`


## Step-by-Step Guide

### Step 1: Assign nb_streamlines = len(...)

```python
nb_streamlines = len(DATA['tractogram'])
```

**Verification:**
```python
assert data_dict.keys() == data_per_streamline.keys()
```

### Step 2: Assign data_per_streamline = value

```python
data_per_streamline = DATA['tractogram'].data_per_streamline
```

**Verification:**
```python
assert_array_equal(data_dict[k], data_per_streamline[k])
```

### Step 3: Assign data_dict = PerArrayDict(...)

```python
data_dict = PerArrayDict(nb_streamlines, data_per_streamline)
```

**Verification:**
```python
assert len(data_dict) == len(data_per_streamline) - 1
```

### Step 4: Assign data_per_streamline = value

```python
data_per_streamline = DATA['data_per_streamline']
```

**Verification:**
```python
assert data_dict.keys() == data_per_streamline.keys()
```

### Step 5: Assign data_dict = PerArrayDict(...)

```python
data_dict = PerArrayDict(nb_streamlines, data_per_streamline)
```

**Verification:**
```python
assert_array_equal(data_dict[k], data_per_streamline[k])
```

### Step 6: Assign data_per_streamline = value

```python
data_per_streamline = DATA['data_per_streamline']
```

**Verification:**
```python
assert len(data_dict) == len(data_per_streamline) - 1
```

### Step 7: Assign data_dict = PerArrayDict(...)

```python
data_dict = PerArrayDict(nb_streamlines, **data_per_streamline)
```

**Verification:**
```python
assert data_dict.keys() == data_per_streamline.keys()
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(data_dict[k], data_per_streamline[k])
```

**Verification:**
```python
assert_array_equal(data_dict[k], data_per_streamline[k])
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal(data_dict[k], data_per_streamline[k])
```

**Verification:**
```python
assert len(data_dict) == len(data_per_streamline) - 1
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(data_dict[k], data_per_streamline[k])
```


## Complete Example

```python
# Workflow
nb_streamlines = len(DATA['tractogram'])
data_per_streamline = DATA['tractogram'].data_per_streamline
data_dict = PerArrayDict(nb_streamlines, data_per_streamline)
assert data_dict.keys() == data_per_streamline.keys()
for k in data_dict.keys():
    if isinstance(data_dict[k], np.ndarray) and np.all(data_dict[k].shape[0] == data_dict[k].shape):
        assert_array_equal(data_dict[k], data_per_streamline[k])
del data_dict['mean_curvature']
assert len(data_dict) == len(data_per_streamline) - 1
data_per_streamline = DATA['data_per_streamline']
data_dict = PerArrayDict(nb_streamlines, data_per_streamline)
assert data_dict.keys() == data_per_streamline.keys()
for k in data_dict.keys():
    if isinstance(data_dict[k], np.ndarray) and np.all(data_dict[k].shape[0] == data_dict[k].shape):
        assert_array_equal(data_dict[k], data_per_streamline[k])
del data_dict['mean_curvature']
assert len(data_dict) == len(data_per_streamline) - 1
data_per_streamline = DATA['data_per_streamline']
data_dict = PerArrayDict(nb_streamlines, **data_per_streamline)
assert data_dict.keys() == data_per_streamline.keys()
for k in data_dict.keys():
    if isinstance(data_dict[k], np.ndarray) and np.all(data_dict[k].shape[0] == data_dict[k].shape):
        assert_array_equal(data_dict[k], data_per_streamline[k])
del data_dict['mean_curvature']
assert len(data_dict) == len(data_per_streamline) - 1
```

## Next Steps


---

*Source: test_tractogram.py:214 | Complexity: Advanced | Last updated: 2026-05-18*