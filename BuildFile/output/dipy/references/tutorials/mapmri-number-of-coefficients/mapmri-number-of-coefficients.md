# How To: Mapmri Number Of Coefficients

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test mapmri number of coefficients

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `math`
- `platform`
- `time`
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `scipy.integrate`
- `scipy.special`
- `dipy.core.sphere_stats`
- `dipy.core.subdivide_octahedron`
- `dipy.data`
- `dipy.direction.peaks`
- `dipy.reconst`
- `dipy.reconst.mapmri`
- `dipy.reconst.odf`
- `dipy.reconst.shm`
- `dipy.reconst.tests.test_dsi`
- `dipy.sims.voxel`
- `dipy.testing.decorators`

**Setup Required:**
```python
# Fixtures: radial_order
```

## Step-by-Step Guide

### Step 1: Assign indices = mapmri_index_matrix(...)

```python
indices = mapmri_index_matrix(radial_order)
```

**Verification:**
```python
assert_equal(n_c, n_gt)
```

### Step 2: Assign n_c = value

```python
n_c = indices.shape[0]
```

### Step 3: Assign F = value

```python
F = radial_order / 2
```

### Step 4: Assign n_gt = np.round(...)

```python
n_gt = np.round(1 / 6.0 * (F + 1) * (F + 2) * (4 * F + 3))
```

### Step 5: Call assert_equal()

```python
assert_equal(n_c, n_gt)
```


## Complete Example

```python
# Setup
# Fixtures: radial_order

# Workflow
indices = mapmri_index_matrix(radial_order)
n_c = indices.shape[0]
F = radial_order / 2
n_gt = np.round(1 / 6.0 * (F + 1) * (F + 2) * (4 * F + 3))
assert_equal(n_c, n_gt)
```

## Next Steps


---

*Source: test_mapmri.py:150 | Complexity: Intermediate | Last updated: 2026-05-18*