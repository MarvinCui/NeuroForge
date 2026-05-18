# How To: Bundlewarp

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test bundlewarp

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
assert_equal(len(affine_bundle), len(cb2))
```

### Step 2: Assign cb1 = Streamlines(...)

```python
cb1 = Streamlines(cingulum_bundles[0])
```

**Verification:**
```python
assert_equal(len(deformed_bundle), len(cb2))
```

### Step 3: Assign cb1 = set_number_of_points(...)

```python
cb1 = set_number_of_points(cb1, nb_points=20)
```

**Verification:**
```python
assert_equal(len(deformed_bundle), len(affine_bundle))
```

### Step 4: Assign cb2 = Streamlines(...)

```python
cb2 = Streamlines(cingulum_bundles[1])
```

**Verification:**
```python
assert_equal(dists.shape, (len(cb2), len(cb1)))
```

### Step 5: Assign cb2 = set_number_of_points(...)

```python
cb2 = set_number_of_points(cb2, nb_points=20)
```

**Verification:**
```python
assert_equal(len(cb2), len(mp))
```

### Step 6: Assign unknown = bundlewarp(...)

```python
deformed_bundle, affine_bundle, dists, mp, warp = bundlewarp(cb1, cb2)
```

**Verification:**
```python
assert_equal(len(cb2), len(warp))
```

### Step 7: Call assert_equal()

```python
assert_equal(len(affine_bundle), len(cb2))
```

### Step 8: Call assert_equal()

```python
assert_equal(len(deformed_bundle), len(cb2))
```

### Step 9: Call assert_equal()

```python
assert_equal(len(deformed_bundle), len(affine_bundle))
```

### Step 10: Call assert_equal()

```python
assert_equal(dists.shape, (len(cb2), len(cb1)))
```

### Step 11: Call assert_equal()

```python
assert_equal(len(cb2), len(mp))
```

### Step 12: Call assert_equal()

```python
assert_equal(len(cb2), len(warp))
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
assert_equal(len(affine_bundle), len(cb2))
assert_equal(len(deformed_bundle), len(cb2))
assert_equal(len(deformed_bundle), len(affine_bundle))
assert_equal(dists.shape, (len(cb2), len(cb1)))
assert_equal(len(cb2), len(mp))
assert_equal(len(cb2), len(warp))
```

## Next Steps


---

*Source: test_streamwarp.py:18 | Complexity: Advanced | Last updated: 2026-05-18*