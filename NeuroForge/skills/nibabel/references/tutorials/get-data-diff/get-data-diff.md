# How To: Get Data Diff

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test get data diff

## Prerequisites

**Required Modules:**
- `io`
- `os.path`
- `numpy`
- `pytest`
- `nibabel`
- `nibabel.cmdline.diff`
- `nibabel.cmdline.utils`
- `nibabel.testing`


## Step-by-Step Guide

### Step 1: Assign test_names = value

```python
test_names = [pjoin(data_path, f) for f in ('standard.nii.gz', 'standard.nii.gz')]
```

**Verification:**
```python
assert get_data_hash_diff(test_names) == []
```

### Step 2: Assign test_array = np.arange.reshape(...)

```python
test_array = np.arange(16).reshape(4, 4)
```

**Verification:**
```python
assert get_data_diff([test_array, test_array_2]) == {'DATA(diff 1:)': [None, {'abs': 1, 'rel': 2.0}]}
```

### Step 3: Assign test_array_2 = np.arange.reshape(...)

```python
test_array_2 = np.arange(1, 17).reshape(4, 4)
```

**Verification:**
```python
assert get_data_diff([test_array, test_array_2, test_array_3]) == {'DATA(diff 1:)': [None, {'abs': 1, 'rel': 2.0}, {'abs': 2, 'rel': 2.0}], 'DATA(diff 2:)': [None, None, {'abs': 1, 'rel': 0.6666666666666666}]}
```

### Step 4: Assign test_array_3 = np.arange.reshape(...)

```python
test_array_3 = np.arange(2, 18).reshape(4, 4)
```

**Verification:**
```python
assert get_data_diff([test_array, test_array_2], max_abs=2, max_rel=2) == {}
```

### Step 5: Assign test_array_4 = np.arange.reshape(...)

```python
test_array_4 = np.arange(100).reshape(10, 10)
```

**Verification:**
```python
assert get_data_diff([test_array_2, test_array_4]) == {'DATA(diff 1:)': [None, {'CMP': 'incompat'}]}
```

### Step 6: Assign test_array_5 = np.arange.reshape(...)

```python
test_array_5 = np.arange(64).reshape(8, 8)
```

**Verification:**
```python
assert get_data_diff([test_array_4, test_array_5, test_array_2]) == {'DATA(diff 1:)': [None, {'CMP': 'incompat'}, {'CMP': 'incompat'}], 'DATA(diff 2:)': [None, None, {'CMP': 'incompat'}]}
```

### Step 7: Assign test_return = get_data_diff(...)

```python
test_return = get_data_diff([test_array, test_array_2], dtype=np.float32)
```

**Verification:**
```python
assert type(test_return['DATA(diff 1:)'][1]['abs']) is np.float32
```

### Step 8: Assign test_return_2 = get_data_diff(...)

```python
test_return_2 = get_data_diff([test_array, test_array_2, test_array_3])
```

**Verification:**
```python
assert type(test_return['DATA(diff 1:)'][1]['rel']) is np.float32
```


## Complete Example

```python
# Workflow
test_names = [pjoin(data_path, f) for f in ('standard.nii.gz', 'standard.nii.gz')]
assert get_data_hash_diff(test_names) == []
test_array = np.arange(16).reshape(4, 4)
test_array_2 = np.arange(1, 17).reshape(4, 4)
test_array_3 = np.arange(2, 18).reshape(4, 4)
test_array_4 = np.arange(100).reshape(10, 10)
test_array_5 = np.arange(64).reshape(8, 8)
assert get_data_diff([test_array, test_array_2]) == {'DATA(diff 1:)': [None, {'abs': 1, 'rel': 2.0}]}
assert get_data_diff([test_array, test_array_2, test_array_3]) == {'DATA(diff 1:)': [None, {'abs': 1, 'rel': 2.0}, {'abs': 2, 'rel': 2.0}], 'DATA(diff 2:)': [None, None, {'abs': 1, 'rel': 0.6666666666666666}]}
assert get_data_diff([test_array, test_array_2], max_abs=2, max_rel=2) == {}
assert get_data_diff([test_array_2, test_array_4]) == {'DATA(diff 1:)': [None, {'CMP': 'incompat'}]}
assert get_data_diff([test_array_4, test_array_5, test_array_2]) == {'DATA(diff 1:)': [None, {'CMP': 'incompat'}, {'CMP': 'incompat'}], 'DATA(diff 2:)': [None, None, {'CMP': 'incompat'}]}
test_return = get_data_diff([test_array, test_array_2], dtype=np.float32)
assert type(test_return['DATA(diff 1:)'][1]['abs']) is np.float32
assert type(test_return['DATA(diff 1:)'][1]['rel']) is np.float32
test_return_2 = get_data_diff([test_array, test_array_2, test_array_3])
assert type(test_return_2['DATA(diff 1:)'][1]['abs']) is np.float64
assert type(test_return_2['DATA(diff 1:)'][1]['rel']) is np.float64
assert type(test_return_2['DATA(diff 2:)'][2]['abs']) is np.float64
assert type(test_return_2['DATA(diff 2:)'][2]['rel']) is np.float64
```

## Next Steps


---

*Source: test_utils.py:191 | Complexity: Advanced | Last updated: 2026-05-18*