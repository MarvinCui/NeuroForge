# How To: Bootstrap Array

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test bootstrap array

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.linalg`
- `numpy.testing`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.core.interpolation`
- `dipy.core.sphere`
- `dipy.data`
- `dipy.direction.peaks`
- `dipy.reconst`
- `dipy.reconst.shm`
- `dipy.sims.voxel`
- `dipy.testing`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign B = np.array(...)

```python
B = np.array([[4, 5, 7, 4, 2.0], [4, 6, 2, 3, 6.0]])
```

**Verification:**
```python
assert_array_almost_equal(bootstrap_data_voxel(dhat, H, R), dhat)
```

### Step 2: Assign H = hat(...)

```python
H = hat(B.T)
```

**Verification:**
```python
assert_array_almost_equal(bootstrap_data_array(dhat, H, R), dhat)
```

### Step 3: Assign R = np.zeros(...)

```python
R = np.zeros((5, 5))
```

### Step 4: Assign d = np.arange(...)

```python
d = np.arange(1, 6)
```

### Step 5: Assign dhat = np.dot(...)

```python
dhat = np.dot(H, d)
```

### Step 6: Call assert_array_almost_equal()

```python
assert_array_almost_equal(bootstrap_data_voxel(dhat, H, R), dhat)
```

### Step 7: Call assert_array_almost_equal()

```python
assert_array_almost_equal(bootstrap_data_array(dhat, H, R), dhat)
```


## Complete Example

```python
# Workflow
B = np.array([[4, 5, 7, 4, 2.0], [4, 6, 2, 3, 6.0]])
H = hat(B.T)
R = np.zeros((5, 5))
d = np.arange(1, 6)
dhat = np.dot(H, d)
assert_array_almost_equal(bootstrap_data_voxel(dhat, H, R), dhat)
assert_array_almost_equal(bootstrap_data_array(dhat, H, R), dhat)
```

## Next Steps


---

*Source: test_shm.py:715 | Complexity: Intermediate | Last updated: 2026-05-18*