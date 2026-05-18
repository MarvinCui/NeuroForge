# How To: Lazydict Creation

**Difficulty**: Beginner
**Estimated Time**: 5 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test lazydict creation

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

### Step 1: Assign lazy_dicts = value

```python
lazy_dicts = []
```

**Verification:**
```python
assert is_lazy_dict(data_dict)
```

### Step 2: Assign expected_keys = unknown.keys(...)

```python
expected_keys = DATA['data_per_streamline_func'].keys()
```

**Verification:**
```python
assert data_dict.keys() == expected_keys
```

### Step 3: Call assert_array_equal()

```python
assert_array_equal(list(data_dict[k]), list(DATA['data_per_streamline'][k]))
```

**Verification:**
```python
assert_array_equal(list(data_dict[k]), list(DATA['data_per_streamline'][k]))
```


## Complete Example

```python
# Workflow
lazy_dicts = []
lazy_dicts += [LazyDict(DATA['data_per_streamline_func'])]
lazy_dicts += [LazyDict(**DATA['data_per_streamline_func'])]
expected_keys = DATA['data_per_streamline_func'].keys()
for data_dict in lazy_dicts:
    assert is_lazy_dict(data_dict)
    assert data_dict.keys() == expected_keys
    for k in data_dict.keys():
        if isinstance(data_dict[k], np.ndarray) and np.all(data_dict[k].shape[0] == data_dict[k].shape):
            assert_array_equal(list(data_dict[k]), list(DATA['data_per_streamline'][k]))
    assert len(data_dict) == len(DATA['data_per_streamline_func'])
```

## Next Steps


---

*Source: test_tractogram.py:450 | Complexity: Beginner | Last updated: 2026-05-18*