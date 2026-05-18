# How To: Patch Radius Accepts Numpy Array

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test patch radius accepts numpy array

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.core.gradients`
- `dipy.denoise`
- `dipy.sims.voxel`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.utils.optpkg`
- `sklearn.dummy`


## Step-by-Step Guide

### Step 1: Assign data = np.random.rand(...)

```python
data = np.random.rand(5, 5, 5, 10)
```

**Verification:**
```python
assert_equal(out_scalar.shape, data.shape)
```

### Step 2: Assign bvals = np.zeros(...)

```python
bvals = np.zeros(10)
```

**Verification:**
```python
assert_equal(out_arr.shape, data.shape)
```

### Step 3: Assign out_scalar = p2s.patch2self(...)

```python
out_scalar = p2s.patch2self(data, bvals, patch_radius=np.array(1), version=1)
```

### Step 4: Call assert_equal()

```python
assert_equal(out_scalar.shape, data.shape)
```

### Step 5: Assign out_arr = p2s.patch2self(...)

```python
out_arr = p2s.patch2self(data, bvals, patch_radius=np.array([1, 1, 1]), version=1)
```

### Step 6: Call assert_equal()

```python
assert_equal(out_arr.shape, data.shape)
```

### Step 7: Call p2s.patch2self()

```python
p2s.patch2self(data, bvals, patch_radius=np.array([1, 1]), version=1)
```


## Complete Example

```python
# Workflow
data = np.random.rand(5, 5, 5, 10)
bvals = np.zeros(10)
out_scalar = p2s.patch2self(data, bvals, patch_radius=np.array(1), version=1)
assert_equal(out_scalar.shape, data.shape)
out_arr = p2s.patch2self(data, bvals, patch_radius=np.array([1, 1, 1]), version=1)
assert_equal(out_arr.shape, data.shape)
with pytest.raises(ValueError, match='patch_radius must be a scalar or a 3-element array.'):
    p2s.patch2self(data, bvals, patch_radius=np.array([1, 1]), version=1)
```

## Next Steps


---

*Source: test_patch2self.py:438 | Complexity: Intermediate | Last updated: 2026-05-18*