# How To: Indexing On Tensor Fit

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test indexing on tensor fit

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

### Step 1: Assign params = np.zeros(...)

```python
params = np.zeros([2, 3, 4, 12])
```

### Step 2: Assign fit = dti.TensorFit(...)

```python
fit = dti.TensorFit(None, params)
```

### Step 3: Call npt.assert_equal()

```python
npt.assert_equal(fit.shape, (2, 3, 4))
```

### Step 4: Assign fit1 = value

```python
fit1 = fit[0]
```

### Step 5: Call npt.assert_equal()

```python
npt.assert_equal(fit1.shape, (3, 4))
```

### Step 6: Call npt.assert_equal()

```python
npt.assert_equal(type(fit1), dti.TensorFit)
```

### Step 7: Assign fit1 = value

```python
fit1 = fit[0, 0, 0]
```

### Step 8: Call npt.assert_equal()

```python
npt.assert_equal(fit1.shape, ())
```

### Step 9: Call npt.assert_equal()

```python
npt.assert_equal(type(fit1), dti.TensorFit)
```

### Step 10: Assign fit1 = value

```python
fit1 = fit[[0], slice(None)]
```

### Step 11: Call npt.assert_equal()

```python
npt.assert_equal(fit1.shape, (1, 3, 4))
```

### Step 12: Call npt.assert_equal()

```python
npt.assert_equal(type(fit1), dti.TensorFit)
```

### Step 13: Call npt.assert_raises()

```python
npt.assert_raises(IndexError, fit.__getitem__, (0, 0, 0, 0))
```


## Complete Example

```python
# Workflow
params = np.zeros([2, 3, 4, 12])
fit = dti.TensorFit(None, params)
npt.assert_equal(fit.shape, (2, 3, 4))
fit1 = fit[0]
npt.assert_equal(fit1.shape, (3, 4))
npt.assert_equal(type(fit1), dti.TensorFit)
fit1 = fit[0, 0, 0]
npt.assert_equal(fit1.shape, ())
npt.assert_equal(type(fit1), dti.TensorFit)
fit1 = fit[[0], slice(None)]
npt.assert_equal(fit1.shape, (1, 3, 4))
npt.assert_equal(type(fit1), dti.TensorFit)
npt.assert_raises(IndexError, fit.__getitem__, (0, 0, 0, 0))
```

## Next Steps


---

*Source: test_dti.py:245 | Complexity: Advanced | Last updated: 2026-05-18*