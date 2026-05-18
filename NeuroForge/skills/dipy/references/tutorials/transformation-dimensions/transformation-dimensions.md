# How To: Transformation Dimensions

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test transformation dimensions

## Prerequisites

**Required Modules:**
- `numpy.testing`
- `pytest`
- `dipy.align.streamwarp`
- `dipy.data`
- `dipy.tracking.streamline`
- `dipy.utils.optpkg`


## Step-by-Step Guide

### Step 1: Assign cingulum_bundles = two_cingulum_bundles(...)

```python
cingulum_bundles = two_cingulum_bundles()
```

**Verification:**
```python
assert_equal(warp['gaussian_kernel'][0].shape, (n, n))
```

### Step 2: Assign n = 20

```python
n = 20
```

**Verification:**
```python
assert_equal(warp['transforms'][0].shape, (n, 3))
```

### Step 3: Assign cb1 = Streamlines(...)

```python
cb1 = Streamlines(cingulum_bundles[0])
```

**Verification:**
```python
assert_equal(warp.columns.get_loc('gaussian_kernel'), 0)
```

### Step 4: Assign cb1 = set_number_of_points(...)

```python
cb1 = set_number_of_points(cb1, n)
```

**Verification:**
```python
assert_equal(warp.columns.get_loc('transforms'), 1)
```

### Step 5: Assign cb2 = Streamlines(...)

```python
cb2 = Streamlines(cingulum_bundles[1])
```

### Step 6: Assign cb2 = set_number_of_points(...)

```python
cb2 = set_number_of_points(cb2, n)
```

### Step 7: Assign unknown = bundlewarp(...)

```python
deformed_bundle, affine_bundle, dists, mp, warp = bundlewarp(cb1, cb2)
```

### Step 8: Call assert_equal()

```python
assert_equal(warp['gaussian_kernel'][0].shape, (n, n))
```

### Step 9: Call assert_equal()

```python
assert_equal(warp['transforms'][0].shape, (n, 3))
```

### Step 10: Call assert_equal()

```python
assert_equal(warp.columns.get_loc('gaussian_kernel'), 0)
```

### Step 11: Call assert_equal()

```python
assert_equal(warp.columns.get_loc('transforms'), 1)
```


## Complete Example

```python
# Workflow
cingulum_bundles = two_cingulum_bundles()
n = 20
cb1 = Streamlines(cingulum_bundles[0])
cb1 = set_number_of_points(cb1, n)
cb2 = Streamlines(cingulum_bundles[1])
cb2 = set_number_of_points(cb2, n)
deformed_bundle, affine_bundle, dists, mp, warp = bundlewarp(cb1, cb2)
assert_equal(warp['gaussian_kernel'][0].shape, (n, n))
assert_equal(warp['transforms'][0].shape, (n, 3))
assert_equal(warp.columns.get_loc('gaussian_kernel'), 0)
assert_equal(warp.columns.get_loc('transforms'), 1)
```

## Next Steps


---

*Source: test_streamwarp.py:95 | Complexity: Advanced | Last updated: 2026-05-18*