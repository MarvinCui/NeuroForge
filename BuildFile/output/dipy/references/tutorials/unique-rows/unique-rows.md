# How To: Unique Rows

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Testing the function unique_coords

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.tracking`
- `dipy.tracking._utils`
- `dipy.tracking.streamline`
- `dipy.tracking.utils`
- `dipy.tracking.vox2track`


## Step-by-Step Guide

### Step 1: '\n    Testing the function unique_coords\n    '

```python
'\n    Testing the function unique_coords\n    '
```

### Step 2: Assign arr = np.array(...)

```python
arr = np.array([[1, 2, 3], [1, 2, 3], [2, 3, 4], [3, 4, 5]])
```

### Step 3: Assign arr_w_unique = np.array(...)

```python
arr_w_unique = np.array([[1, 2, 3], [2, 3, 4], [3, 4, 5]])
```

### Step 4: Call npt.assert_array_equal()

```python
npt.assert_array_equal(unique_rows(arr), arr_w_unique)
```

### Step 5: Assign arr = np.array(...)

```python
arr = np.array([[2, 3, 4], [1, 2, 3], [1, 2, 3], [3, 4, 5]])
```

### Step 6: Assign arr_w_unique = np.array(...)

```python
arr_w_unique = np.array([[2, 3, 4], [1, 2, 3], [3, 4, 5]])
```

### Step 7: Call npt.assert_array_equal()

```python
npt.assert_array_equal(unique_rows(arr), arr_w_unique)
```

### Step 8: Assign arr = np.array(...)

```python
arr = np.array([[2, 3, 4], [1, 2, 3], [1, 2, 3], [3, 4, 5], [6, 7, 8], [0, 1, 0], [1, 0, 1]])
```

### Step 9: Assign arr_w_unique = np.array(...)

```python
arr_w_unique = np.array([[2, 3, 4], [1, 2, 3], [3, 4, 5], [6, 7, 8], [0, 1, 0], [1, 0, 1]])
```

### Step 10: Call npt.assert_array_equal()

```python
npt.assert_array_equal(unique_rows(arr), arr_w_unique)
```


## Complete Example

```python
# Workflow
'\n    Testing the function unique_coords\n    '
arr = np.array([[1, 2, 3], [1, 2, 3], [2, 3, 4], [3, 4, 5]])
arr_w_unique = np.array([[1, 2, 3], [2, 3, 4], [3, 4, 5]])
npt.assert_array_equal(unique_rows(arr), arr_w_unique)
arr = np.array([[2, 3, 4], [1, 2, 3], [1, 2, 3], [3, 4, 5]])
arr_w_unique = np.array([[2, 3, 4], [1, 2, 3], [3, 4, 5]])
npt.assert_array_equal(unique_rows(arr), arr_w_unique)
arr = np.array([[2, 3, 4], [1, 2, 3], [1, 2, 3], [3, 4, 5], [6, 7, 8], [0, 1, 0], [1, 0, 1]])
arr_w_unique = np.array([[2, 3, 4], [1, 2, 3], [3, 4, 5], [6, 7, 8], [0, 1, 0], [1, 0, 1]])
npt.assert_array_equal(unique_rows(arr), arr_w_unique)
```

## Next Steps


---

*Source: test_utils.py:759 | Complexity: Advanced | Last updated: 2026-05-18*