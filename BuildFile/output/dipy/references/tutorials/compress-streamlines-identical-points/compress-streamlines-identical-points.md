# How To: Compress Streamlines Identical Points

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test compress streamlines identical points

## Prerequisites

**Required Modules:**
- `types`
- `warnings`
- `numpy`
- `numpy.linalg`
- `numpy.testing`
- `numpy.testing`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.testing.memory`
- `dipy.tracking.streamline`
- `dipy.tracking.streamlinespeed`


## Step-by-Step Guide

### Step 1: Assign sl_1 = np.array(...)

```python
sl_1 = np.array([[1, 1, 1], [1, 1, 1], [2, 2, 2], [3, 3, 3], [3, 3, 3]])
```

### Step 2: Assign sl_2 = np.array(...)

```python
sl_2 = np.array([[1, 1, 1], [1, 1, 1], [1, 1, 1], [2, 2, 2]])
```

### Step 3: Assign sl_3 = np.array(...)

```python
sl_3 = np.array([[1, 1, 1], [1, 1, 1], [1, 1, 1], [1, 1, 1], [2, 2, 2], [2, 2, 2], [2, 2, 2], [3, 3, 3], [3, 3, 3]])
```

### Step 4: Assign sl_4 = np.array(...)

```python
sl_4 = np.array([[1, 1, 1], [1, 1, 1], [1, 1, 1], [1, 1, 1], [2, 2, 2], [3, 3, 3], [3, 3, 3], [1, 1, 1]])
```

### Step 5: Assign new_sl_1 = compress_streamlines(...)

```python
new_sl_1 = compress_streamlines(sl_1)
```

### Step 6: Assign new_sl_2 = compress_streamlines(...)

```python
new_sl_2 = compress_streamlines(sl_2)
```

### Step 7: Assign new_sl_3 = compress_streamlines(...)

```python
new_sl_3 = compress_streamlines(sl_3)
```

### Step 8: Assign new_sl_4 = compress_streamlines(...)

```python
new_sl_4 = compress_streamlines(sl_4)
```

### Step 9: Call npt.assert_array_equal()

```python
npt.assert_array_equal(new_sl_1, np.array([[1, 1, 1], [3, 3, 3]]))
```

### Step 10: Call npt.assert_array_equal()

```python
npt.assert_array_equal(new_sl_2, np.array([[1, 1, 1], [2, 2, 2]]))
```

### Step 11: Call npt.assert_array_equal()

```python
npt.assert_array_equal(new_sl_3, new_sl_1)
```

### Step 12: Call npt.assert_array_equal()

```python
npt.assert_array_equal(new_sl_4, np.array([[1, 1, 1], [3, 3, 3], [1, 1, 1]]))
```


## Complete Example

```python
# Workflow
sl_1 = np.array([[1, 1, 1], [1, 1, 1], [2, 2, 2], [3, 3, 3], [3, 3, 3]])
sl_2 = np.array([[1, 1, 1], [1, 1, 1], [1, 1, 1], [2, 2, 2]])
sl_3 = np.array([[1, 1, 1], [1, 1, 1], [1, 1, 1], [1, 1, 1], [2, 2, 2], [2, 2, 2], [2, 2, 2], [3, 3, 3], [3, 3, 3]])
sl_4 = np.array([[1, 1, 1], [1, 1, 1], [1, 1, 1], [1, 1, 1], [2, 2, 2], [3, 3, 3], [3, 3, 3], [1, 1, 1]])
new_sl_1 = compress_streamlines(sl_1)
new_sl_2 = compress_streamlines(sl_2)
new_sl_3 = compress_streamlines(sl_3)
new_sl_4 = compress_streamlines(sl_4)
npt.assert_array_equal(new_sl_1, np.array([[1, 1, 1], [3, 3, 3]]))
npt.assert_array_equal(new_sl_2, np.array([[1, 1, 1], [2, 2, 2]]))
npt.assert_array_equal(new_sl_3, new_sl_1)
npt.assert_array_equal(new_sl_4, np.array([[1, 1, 1], [3, 3, 3], [1, 1, 1]]))
```

## Next Steps


---

*Source: test_streamline.py:795 | Complexity: Advanced | Last updated: 2026-05-18*