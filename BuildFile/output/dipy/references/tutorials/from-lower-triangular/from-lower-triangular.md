# How To: From Lower Triangular

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test from lower triangular

## Prerequisites

**Required Modules:**
- `random`
- `numpy`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.core.sphere`
- `dipy.core.subdivide_octahedron`
- `dipy.data`
- `dipy.io.gradients`
- `dipy.io.image`
- `dipy.reconst.dti`
- `dipy.reconst.dti`
- `dipy.reconst.weights_method`
- `dipy.sims.voxel`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.utils.optpkg`


## Step-by-Step Guide

### Step 1: Assign result = np.array(...)

```python
result = np.array([[0, 1, 3], [1, 2, 4], [3, 4, 5]])
```

### Step 2: Assign D = np.arange(...)

```python
D = np.arange(7)
```

### Step 3: Assign tensor = from_lower_triangular(...)

```python
tensor = from_lower_triangular(D)
```

### Step 4: Call npt.assert_array_equal()

```python
npt.assert_array_equal(tensor, result)
```

### Step 5: Assign result = value

```python
result = result * np.ones((5, 4, 1, 1))
```

### Step 6: Assign D = value

```python
D = D * np.ones((5, 4, 1))
```

### Step 7: Assign tensor = from_lower_triangular(...)

```python
tensor = from_lower_triangular(D)
```

### Step 8: Call npt.assert_array_equal()

```python
npt.assert_array_equal(tensor, result)
```


## Complete Example

```python
# Workflow
result = np.array([[0, 1, 3], [1, 2, 4], [3, 4, 5]])
D = np.arange(7)
tensor = from_lower_triangular(D)
npt.assert_array_equal(tensor, result)
result = result * np.ones((5, 4, 1, 1))
D = D * np.ones((5, 4, 1))
tensor = from_lower_triangular(D)
npt.assert_array_equal(tensor, result)
```

## Next Steps


---

*Source: test_dti.py:649 | Complexity: Advanced | Last updated: 2026-05-18*