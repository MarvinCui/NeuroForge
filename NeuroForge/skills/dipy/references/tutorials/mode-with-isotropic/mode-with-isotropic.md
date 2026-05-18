# How To: Mode With Isotropic

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test mode with isotropic

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

### Step 1: Assign q_form = np.zeros(...)

```python
q_form = np.zeros((2, 2, 3, 3))
```

### Step 2: Assign unknown = 1

```python
q_form[0, 1, 0, 0] = 1
```

### Step 3: Assign unknown = 1

```python
q_form[0, 1, 1, 1] = 1
```

### Step 4: Assign unknown = 1

```python
q_form[0, 1, 2, 2] = 1
```

### Step 5: Assign unknown = 1

```python
q_form[1, 0, 0, 0] = 1
```

### Step 6: Assign unknown = 1

```python
q_form[1, 0, 1, 1] = 1
```

### Step 7: Assign unknown = 2

```python
q_form[1, 0, 2, 2] = 2
```

### Step 8: Assign unknown = 1

```python
q_form[1, 1, 0, 0] = 1
```

### Step 9: Assign unknown = 2

```python
q_form[1, 1, 1, 1] = 2
```

### Step 10: Assign unknown = 2

```python
q_form[1, 1, 2, 2] = 2
```

### Step 11: Call npt.assert_array_almost_equal()

```python
npt.assert_array_almost_equal(mode(q_form), np.array([[0, 0], [1, -1]]))
```


## Complete Example

```python
# Workflow
q_form = np.zeros((2, 2, 3, 3))
q_form[0, 1, 0, 0] = 1
q_form[0, 1, 1, 1] = 1
q_form[0, 1, 2, 2] = 1
q_form[1, 0, 0, 0] = 1
q_form[1, 0, 1, 1] = 1
q_form[1, 0, 2, 2] = 2
q_form[1, 1, 0, 0] = 1
q_form[1, 1, 1, 1] = 2
q_form[1, 1, 2, 2] = 2
npt.assert_array_almost_equal(mode(q_form), np.array([[0, 0], [1, -1]]))
```

## Next Steps


---

*Source: test_dti.py:79 | Complexity: Advanced | Last updated: 2026-05-18*