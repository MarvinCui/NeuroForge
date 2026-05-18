# How To: Create Patch Radius Arr

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test create patch radius arr

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `scipy.special`
- `dipy.core.gradients`
- `dipy.denoise.localpca`
- `dipy.sims.voxel`
- `dipy.testing`
- `dipy.testing.decorators`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign shape = value

```python
shape = (10, 10, 8, 104)
```

**Verification:**
```python
assert np.array_equal(obtained_val, expected_val)
```

### Step 2: Assign arr = rng.standard_normal(...)

```python
arr = rng.standard_normal(shape)
```

### Step 3: Assign pr = 2

```python
pr = 2
```

### Step 4: Assign expected_val = np.asarray(...)

```python
expected_val = np.asarray([2, 2, 2])
```

### Step 5: Assign obtained_val = create_patch_radius_arr(...)

```python
obtained_val = create_patch_radius_arr(arr, pr)
```

**Verification:**
```python
assert np.array_equal(obtained_val, expected_val)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
shape = (10, 10, 8, 104)
arr = rng.standard_normal(shape)
pr = 2
expected_val = np.asarray([2, 2, 2])
obtained_val = create_patch_radius_arr(arr, pr)
assert np.array_equal(obtained_val, expected_val)
```

## Next Steps


---

*Source: test_lpca.py:440 | Complexity: Intermediate | Last updated: 2026-05-18*