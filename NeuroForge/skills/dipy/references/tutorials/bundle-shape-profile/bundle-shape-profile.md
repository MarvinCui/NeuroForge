# How To: Bundle Shape Profile

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test bundle shape profile

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
assert_equal(len(shape_profile), n)
```

### Step 2: Assign cb1 = Streamlines(...)

```python
cb1 = Streamlines(cingulum_bundles[0])
```

**Verification:**
```python
assert_equal(len(stdv), n)
```

### Step 3: Assign cb1 = set_number_of_points(...)

```python
cb1 = set_number_of_points(cb1, nb_points=20)
```

**Verification:**
```python
assert_equal(len(shape_profile), n)
```

### Step 4: Assign cb2 = Streamlines(...)

```python
cb2 = Streamlines(cingulum_bundles[1])
```

**Verification:**
```python
assert_equal(len(stdv), n)
```

### Step 5: Assign cb2 = set_number_of_points(...)

```python
cb2 = set_number_of_points(cb2, nb_points=20)
```

### Step 6: Assign unknown = bundlewarp(...)

```python
deformed_bundle, affine_bundle, dists, mp, warp = bundlewarp(cb1, cb2)
```

### Step 7: Assign n = 10

```python
n = 10
```

### Step 8: Assign unknown = bundlewarp_shape_analysis(...)

```python
shape_profile, stdv = bundlewarp_shape_analysis(Streamlines(affine_bundle), Streamlines(deformed_bundle), no_disks=n)
```

### Step 9: Call assert_equal()

```python
assert_equal(len(shape_profile), n)
```

### Step 10: Call assert_equal()

```python
assert_equal(len(stdv), n)
```

### Step 11: Assign n = 100

```python
n = 100
```

### Step 12: Assign unknown = bundlewarp_shape_analysis(...)

```python
shape_profile, stdv = bundlewarp_shape_analysis(affine_bundle, deformed_bundle, no_disks=n)
```

### Step 13: Call assert_equal()

```python
assert_equal(len(shape_profile), n)
```

### Step 14: Call assert_equal()

```python
assert_equal(len(stdv), n)
```


## Complete Example

```python
# Workflow
cingulum_bundles = two_cingulum_bundles()
cb1 = Streamlines(cingulum_bundles[0])
cb1 = set_number_of_points(cb1, nb_points=20)
cb2 = Streamlines(cingulum_bundles[1])
cb2 = set_number_of_points(cb2, nb_points=20)
deformed_bundle, affine_bundle, dists, mp, warp = bundlewarp(cb1, cb2)
n = 10
shape_profile, stdv = bundlewarp_shape_analysis(Streamlines(affine_bundle), Streamlines(deformed_bundle), no_disks=n)
assert_equal(len(shape_profile), n)
assert_equal(len(stdv), n)
n = 100
shape_profile, stdv = bundlewarp_shape_analysis(affine_bundle, deformed_bundle, no_disks=n)
assert_equal(len(shape_profile), n)
assert_equal(len(stdv), n)
```

## Next Steps


---

*Source: test_streamwarp.py:66 | Complexity: Advanced | Last updated: 2026-05-18*