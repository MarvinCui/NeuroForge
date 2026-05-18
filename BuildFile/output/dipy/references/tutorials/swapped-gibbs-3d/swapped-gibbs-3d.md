# How To: Swapped Gibbs 3D

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test swapped gibbs 3d

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.denoise.gibbs`


## Step-by-Step Guide

### Step 1: Assign image3d = np.zeros(...)

```python
image3d = np.zeros((6 * Nre, 2, 6 * Nre))
```

**Verification:**
```python
assert_array_almost_equal(image3d_cor[:, 0, :], image_cor)
```

### Step 2: Assign unknown = image_gibbs

```python
image3d[:, 0, :] = image_gibbs
```

**Verification:**
```python
assert_array_almost_equal(image3d_cor[:, 1, :], image_cor)
```

### Step 3: Assign unknown = image_gibbs

```python
image3d[:, 1, :] = image_gibbs
```

**Verification:**
```python
assert_array_almost_equal(image3d_cor[0, :, :], image_cor)
```

### Step 4: Assign image3d_cor = gibbs_removal(...)

```python
image3d_cor = gibbs_removal(image3d, slice_axis=1)
```

**Verification:**
```python
assert_array_almost_equal(image3d_cor[1, :, :], image_cor)
```

### Step 5: Call assert_array_almost_equal()

```python
assert_array_almost_equal(image3d_cor[:, 0, :], image_cor)
```

### Step 6: Call assert_array_almost_equal()

```python
assert_array_almost_equal(image3d_cor[:, 1, :], image_cor)
```

### Step 7: Assign image3d = np.zeros(...)

```python
image3d = np.zeros((2, 6 * Nre, 6 * Nre))
```

### Step 8: Assign unknown = image_gibbs

```python
image3d[0, :, :] = image_gibbs
```

### Step 9: Assign unknown = image_gibbs

```python
image3d[1, :, :] = image_gibbs
```

### Step 10: Assign image3d_cor = gibbs_removal(...)

```python
image3d_cor = gibbs_removal(image3d, slice_axis=0)
```

### Step 11: Call assert_array_almost_equal()

```python
assert_array_almost_equal(image3d_cor[0, :, :], image_cor)
```

### Step 12: Call assert_array_almost_equal()

```python
assert_array_almost_equal(image3d_cor[1, :, :], image_cor)
```


## Complete Example

```python
# Workflow
image3d = np.zeros((6 * Nre, 2, 6 * Nre))
image3d[:, 0, :] = image_gibbs
image3d[:, 1, :] = image_gibbs
image3d_cor = gibbs_removal(image3d, slice_axis=1)
assert_array_almost_equal(image3d_cor[:, 0, :], image_cor)
assert_array_almost_equal(image3d_cor[:, 1, :], image_cor)
image3d = np.zeros((2, 6 * Nre, 6 * Nre))
image3d[0, :, :] = image_gibbs
image3d[1, :, :] = image_gibbs
image3d_cor = gibbs_removal(image3d, slice_axis=0)
assert_array_almost_equal(image3d_cor[0, :, :], image_cor)
assert_array_almost_equal(image3d_cor[1, :, :], image_cor)
```

## Next Steps


---

*Source: test_gibbs.py:145 | Complexity: Advanced | Last updated: 2026-05-18*