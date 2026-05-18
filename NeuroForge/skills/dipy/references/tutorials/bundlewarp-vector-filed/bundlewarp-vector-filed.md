# How To: Bundlewarp Vector Filed

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test bundlewarp vector filed

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
assert_equal(len(offsets), len(cb2.get_data()))
```

### Step 2: Assign cb1 = Streamlines(...)

```python
cb1 = Streamlines(cingulum_bundles[0])
```

**Verification:**
```python
assert_equal(len(directions), len(cb2.get_data()))
```

### Step 3: Assign cb1 = set_number_of_points(...)

```python
cb1 = set_number_of_points(cb1, nb_points=20)
```

**Verification:**
```python
assert_equal(len(colors), len(cb2.get_data()))
```

### Step 4: Assign cb2 = Streamlines(...)

```python
cb2 = Streamlines(cingulum_bundles[1])
```

**Verification:**
```python
assert_equal(len(offsets), len(deformed_bundle.get_data()))
```

### Step 5: Assign cb2 = set_number_of_points(...)

```python
cb2 = set_number_of_points(cb2, nb_points=20)
```

**Verification:**
```python
assert_equal(len(directions), len(deformed_bundle.get_data()))
```

### Step 6: Assign unknown = bundlewarp(...)

```python
deformed_bundle, affine_bundle, dists, mp, warp = bundlewarp(cb1, cb2)
```

**Verification:**
```python
assert_equal(len(colors), len(deformed_bundle.get_data()))
```

### Step 7: Assign unknown = bundlewarp_vector_filed(...)

```python
offsets, directions, colors = bundlewarp_vector_filed(affine_bundle, deformed_bundle)
```

### Step 8: Call assert_equal()

```python
assert_equal(len(offsets), len(cb2.get_data()))
```

### Step 9: Call assert_equal()

```python
assert_equal(len(directions), len(cb2.get_data()))
```

### Step 10: Call assert_equal()

```python
assert_equal(len(colors), len(cb2.get_data()))
```

### Step 11: Call assert_equal()

```python
assert_equal(len(offsets), len(deformed_bundle.get_data()))
```

### Step 12: Call assert_equal()

```python
assert_equal(len(directions), len(deformed_bundle.get_data()))
```

### Step 13: Call assert_equal()

```python
assert_equal(len(colors), len(deformed_bundle.get_data()))
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
offsets, directions, colors = bundlewarp_vector_filed(affine_bundle, deformed_bundle)
assert_equal(len(offsets), len(cb2.get_data()))
assert_equal(len(directions), len(cb2.get_data()))
assert_equal(len(colors), len(cb2.get_data()))
assert_equal(len(offsets), len(deformed_bundle.get_data()))
assert_equal(len(directions), len(deformed_bundle.get_data()))
assert_equal(len(colors), len(deformed_bundle.get_data()))
```

## Next Steps


---

*Source: test_streamwarp.py:41 | Complexity: Advanced | Last updated: 2026-05-18*