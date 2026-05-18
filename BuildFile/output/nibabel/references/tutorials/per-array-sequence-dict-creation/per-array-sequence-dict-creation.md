# How To: Per Array Sequence Dict Creation

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test per array sequence dict creation

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

### Step 1: Assign total_nb_rows = value

```python
total_nb_rows = DATA['tractogram'].streamlines.total_nb_rows
```

**Verification:**
```python
assert data_dict.keys() == data_per_point.keys()
```

### Step 2: Assign data_per_point = value

```python
data_per_point = DATA['tractogram'].data_per_point
```

**Verification:**
```python
assert_arrays_equal(data_dict[k], data_per_point[k])
```

### Step 3: Assign data_dict = PerArraySequenceDict(...)

```python
data_dict = PerArraySequenceDict(total_nb_rows, data_per_point)
```

**Verification:**
```python
assert len(data_dict) == len(data_per_point) - 1
```

### Step 4: Assign data_per_point = value

```python
data_per_point = DATA['data_per_point']
```

**Verification:**
```python
assert data_dict.keys() == data_per_point.keys()
```

### Step 5: Assign data_dict = PerArraySequenceDict(...)

```python
data_dict = PerArraySequenceDict(total_nb_rows, data_per_point)
```

**Verification:**
```python
assert_arrays_equal(data_dict[k], data_per_point[k])
```

### Step 6: Assign data_per_point = value

```python
data_per_point = DATA['data_per_point']
```

**Verification:**
```python
assert len(data_dict) == len(data_per_point) - 1
```

### Step 7: Assign data_dict = PerArraySequenceDict(...)

```python
data_dict = PerArraySequenceDict(total_nb_rows, **data_per_point)
```

**Verification:**
```python
assert data_dict.keys() == data_per_point.keys()
```

### Step 8: Call assert_arrays_equal()

```python
assert_arrays_equal(data_dict[k], data_per_point[k])
```

**Verification:**
```python
assert_arrays_equal(data_dict[k], data_per_point[k])
```

### Step 9: Call assert_arrays_equal()

```python
assert_arrays_equal(data_dict[k], data_per_point[k])
```

**Verification:**
```python
assert len(data_dict) == len(data_per_point) - 1
```

### Step 10: Call assert_arrays_equal()

```python
assert_arrays_equal(data_dict[k], data_per_point[k])
```


## Complete Example

```python
# Workflow
total_nb_rows = DATA['tractogram'].streamlines.total_nb_rows
data_per_point = DATA['tractogram'].data_per_point
data_dict = PerArraySequenceDict(total_nb_rows, data_per_point)
assert data_dict.keys() == data_per_point.keys()
for k in data_dict.keys():
    assert_arrays_equal(data_dict[k], data_per_point[k])
del data_dict['fa']
assert len(data_dict) == len(data_per_point) - 1
data_per_point = DATA['data_per_point']
data_dict = PerArraySequenceDict(total_nb_rows, data_per_point)
assert data_dict.keys() == data_per_point.keys()
for k in data_dict.keys():
    assert_arrays_equal(data_dict[k], data_per_point[k])
del data_dict['fa']
assert len(data_dict) == len(data_per_point) - 1
data_per_point = DATA['data_per_point']
data_dict = PerArraySequenceDict(total_nb_rows, **data_per_point)
assert data_dict.keys() == data_per_point.keys()
for k in data_dict.keys():
    assert_arrays_equal(data_dict[k], data_per_point[k])
del data_dict['fa']
assert len(data_dict) == len(data_per_point) - 1
```

## Next Steps


---

*Source: test_tractogram.py:332 | Complexity: Advanced | Last updated: 2026-05-18*