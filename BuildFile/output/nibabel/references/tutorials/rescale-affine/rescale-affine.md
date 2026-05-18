# How To: Rescale Affine

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test rescale affine

## Prerequisites

**Required Modules:**
- `itertools`
- `numpy`
- `pytest`
- `numpy.testing`
- `affines`
- `eulerangles`
- `orientations`
- `math`


## Step-by-Step Guide

### Step 1: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(20200415)
```

**Verification:**
```python
assert aff2axcodes(new_aff) == orig_axcodes
```

### Step 2: Assign orig_shape = rng.randint(...)

```python
orig_shape = rng.randint(low=20, high=512, size=(3,))
```

**Verification:**
```python
assert_almost_equal(new_centroid, orig_centroid)
```

### Step 3: Assign orig_aff = np.eye(...)

```python
orig_aff = np.eye(4)
```

### Step 4: Assign unknown = rng.normal(...)

```python
orig_aff[:3, :] = rng.normal(size=(3, 4))
```

### Step 5: Assign orig_axcodes = aff2axcodes(...)

```python
orig_axcodes = aff2axcodes(orig_aff)
```

### Step 6: Assign orig_centroid = apply_affine(...)

```python
orig_centroid = apply_affine(orig_aff, (orig_shape - 1) // 2)
```

### Step 7: Assign new_aff = rescale_affine(...)

```python
new_aff = rescale_affine(orig_aff, orig_shape, new_zooms, new_shape)
```

**Verification:**
```python
assert aff2axcodes(new_aff) == orig_axcodes
```

### Step 8: Assign new_centroid = apply_affine(...)

```python
new_centroid = apply_affine(new_aff, (np.array(new_shape) - 1) // 2)
```

### Step 9: Call assert_almost_equal()

```python
assert_almost_equal(new_centroid, orig_centroid)
```

### Step 10: Assign new_shape = tuple(...)

```python
new_shape = tuple(orig_shape)
```


## Complete Example

```python
# Workflow
rng = np.random.RandomState(20200415)
orig_shape = rng.randint(low=20, high=512, size=(3,))
orig_aff = np.eye(4)
orig_aff[:3, :] = rng.normal(size=(3, 4))
orig_axcodes = aff2axcodes(orig_aff)
orig_centroid = apply_affine(orig_aff, (orig_shape - 1) // 2)
for new_shape in (None, tuple(orig_shape), (256, 256, 256), (64, 64, 40)):
    for new_zooms in ((1, 1, 1), (2, 2, 3), (0.5, 0.5, 0.5)):
        new_aff = rescale_affine(orig_aff, orig_shape, new_zooms, new_shape)
        assert aff2axcodes(new_aff) == orig_axcodes
        if new_shape is None:
            new_shape = tuple(orig_shape)
        new_centroid = apply_affine(new_aff, (np.array(new_shape) - 1) // 2)
        assert_almost_equal(new_centroid, orig_centroid)
```

## Next Steps


---

*Source: test_affines.py:223 | Complexity: Advanced | Last updated: 2026-05-18*