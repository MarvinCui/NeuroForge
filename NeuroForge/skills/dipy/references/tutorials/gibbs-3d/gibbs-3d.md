# How To: Gibbs 3D

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test gibbs 3d

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.denoise.gibbs`


## Step-by-Step Guide

### Step 1: Assign image3d = np.zeros(...)

```python
image3d = np.zeros((6 * Nre, 6 * Nre, 2))
```

**Verification:**
```python
assert_array_almost_equal(image3d_cor[:, :, 0], image_cor)
```

### Step 2: Assign unknown = image_gibbs

```python
image3d[:, :, 0] = image_gibbs
```

**Verification:**
```python
assert_array_almost_equal(image3d_cor[:, :, 1], image_cor)
```

### Step 3: Assign unknown = image_gibbs

```python
image3d[:, :, 1] = image_gibbs
```

### Step 4: Assign image3d_cor = gibbs_removal(...)

```python
image3d_cor = gibbs_removal(image3d, slice_axis=2)
```

### Step 5: Call assert_array_almost_equal()

```python
assert_array_almost_equal(image3d_cor[:, :, 0], image_cor)
```

### Step 6: Call assert_array_almost_equal()

```python
assert_array_almost_equal(image3d_cor[:, :, 1], image_cor)
```


## Complete Example

```python
# Workflow
image3d = np.zeros((6 * Nre, 6 * Nre, 2))
image3d[:, :, 0] = image_gibbs
image3d[:, :, 1] = image_gibbs
image3d_cor = gibbs_removal(image3d, slice_axis=2)
assert_array_almost_equal(image3d_cor[:, :, 0], image_cor)
assert_array_almost_equal(image3d_cor[:, :, 1], image_cor)
```

## Next Steps


---

*Source: test_gibbs.py:108 | Complexity: Intermediate | Last updated: 2026-05-18*