# How To: Resample Vector Field 3D

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Expand a vector field by 2, then subsample by 2, the resulting
field should be the original one

## Prerequisites

**Required Modules:**
- `nibabel.affines`
- `numpy`
- `numpy.testing`
- `scipy.ndimage`
- `dipy.align`
- `dipy.align.parzenhist`
- `dipy.align.transforms`
- `dipy.core`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: '\n    Expand a vector field by 2, then subsample by 2, the resulting\n    field should be the original one\n    '

```python
'\n    Expand a vector field by 2, then subsample by 2, the resulting\n    field should be the original one\n    '
```

**Verification:**
```python
assert_array_almost_equal(d, subsampled)
```

### Step 2: Assign domain_shape = np.array(...)

```python
domain_shape = np.array((64, 64, 64), dtype=np.int32)
```

### Step 3: Assign reduced_shape = np.array(...)

```python
reduced_shape = np.array((32, 32, 32), dtype=np.int32)
```

### Step 4: Assign factors = np.array(...)

```python
factors = np.array([0.5, 0.5, 0.5])
```

### Step 5: Assign unknown = vfu.create_harmonic_fields_3d(...)

```python
d, dinv = vfu.create_harmonic_fields_3d(reduced_shape[0], reduced_shape[1], reduced_shape[2], 0.3, 6)
```

### Step 6: Assign d = np.array(...)

```python
d = np.array(d, dtype=floating)
```

### Step 7: Assign expanded = vfu.resample_displacement_field_3d(...)

```python
expanded = vfu.resample_displacement_field_3d(d, factors, domain_shape)
```

### Step 8: Assign subsampled = value

```python
subsampled = expanded[::2, ::2, ::2, :]
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(d, subsampled)
```


## Complete Example

```python
# Workflow
'\n    Expand a vector field by 2, then subsample by 2, the resulting\n    field should be the original one\n    '
domain_shape = np.array((64, 64, 64), dtype=np.int32)
reduced_shape = np.array((32, 32, 32), dtype=np.int32)
factors = np.array([0.5, 0.5, 0.5])
d, dinv = vfu.create_harmonic_fields_3d(reduced_shape[0], reduced_shape[1], reduced_shape[2], 0.3, 6)
d = np.array(d, dtype=floating)
expanded = vfu.resample_displacement_field_3d(d, factors, domain_shape)
subsampled = expanded[::2, ::2, ::2, :]
assert_array_almost_equal(d, subsampled)
```

## Next Steps


---

*Source: test_vector_fields.py:1319 | Complexity: Advanced | Last updated: 2026-05-18*