# How To: Design Matrix

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test QTI design matrix calculation.

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.core.sphere`
- `dipy.reconst.dti`
- `dipy.reconst.dti`
- `dipy.reconst.qti`
- `dipy.reconst.weights_method`
- `dipy.sims.voxel`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.utils.optpkg`


## Step-by-Step Guide

### Step 1: 'Test QTI design matrix calculation.'

```python
'Test QTI design matrix calculation.'
```

### Step 2: Assign btens = np.array(...)

```python
btens = np.array([np.eye(3, 3) for i in range(3)])
```

### Step 3: Assign unknown = 0

```python
btens[0, 1, 1] = 0
```

### Step 4: Assign unknown = 0

```python
btens[0, 2, 2] = 0
```

### Step 5: Assign unknown = 0

```python
btens[1, 0, 0] = 0
```

### Step 6: Assign X = qti.design_matrix(...)

```python
X = qti.design_matrix(btens)
```

### Step 7: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(X, np.array([[1.0, 1.0, 1.0], [-1.0, -0.0, -1.0], [-0.0, -1.0, -1.0], [-0.0, -1.0, -1.0], [-0.0, -0.0, -0.0], [-0.0, -0.0, -0.0], [-0.0, -0.0, -0.0], [0.5, 0.0, 0.5], [0.0, 0.5, 0.5], [0.0, 0.5, 0.5], [0.0, 0.70710678, 0.70710678], [0.0, 0.0, 0.70710678], [0.0, 0.0, 0.70710678], [0.0, 0.0, 0.0], [0.0, 0.0, 0.0], [0.0, 0.0, 0.0], [0.0, 0.0, 0.0], [0.0, 0.0, 0.0], [0.0, 0.0, 0.0], [0.0, 0.0, 0.0], [0.0, 0.0, 0.0], [0.0, 0.0, 0.0], [0.0, 0.0, 0.0], [0.0, 0.0, 0.0], [0.0, 0.0, 0.0], [0.0, 0.0, 0.0], [0.0, 0.0, 0.0], [0.0, 0.0, 0.0]]).T)
```


## Complete Example

```python
# Workflow
'Test QTI design matrix calculation.'
btens = np.array([np.eye(3, 3) for i in range(3)])
btens[0, 1, 1] = 0
btens[0, 2, 2] = 0
btens[1, 0, 0] = 0
X = qti.design_matrix(btens)
npt.assert_almost_equal(X, np.array([[1.0, 1.0, 1.0], [-1.0, -0.0, -1.0], [-0.0, -1.0, -1.0], [-0.0, -1.0, -1.0], [-0.0, -0.0, -0.0], [-0.0, -0.0, -0.0], [-0.0, -0.0, -0.0], [0.5, 0.0, 0.5], [0.0, 0.5, 0.5], [0.0, 0.5, 0.5], [0.0, 0.70710678, 0.70710678], [0.0, 0.0, 0.70710678], [0.0, 0.0, 0.70710678], [0.0, 0.0, 0.0], [0.0, 0.0, 0.0], [0.0, 0.0, 0.0], [0.0, 0.0, 0.0], [0.0, 0.0, 0.0], [0.0, 0.0, 0.0], [0.0, 0.0, 0.0], [0.0, 0.0, 0.0], [0.0, 0.0, 0.0], [0.0, 0.0, 0.0], [0.0, 0.0, 0.0], [0.0, 0.0, 0.0], [0.0, 0.0, 0.0], [0.0, 0.0, 0.0], [0.0, 0.0, 0.0]]).T)
```

## Next Steps


---

*Source: test_qti.py:263 | Complexity: Intermediate | Last updated: 2026-05-18*