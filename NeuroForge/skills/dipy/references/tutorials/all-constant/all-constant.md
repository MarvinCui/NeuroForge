# How To: All Constant

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test all constant

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

### Step 1: Assign unknown = read_bvals_bvecs(...)

```python
bvals, bvecs = read_bvals_bvecs(*get_fnames(name='55dir_grad'))
```

### Step 2: Assign gtab = grad.gradient_table_from_bvals_bvecs(...)

```python
gtab = grad.gradient_table_from_bvals_bvecs(bvals, bvecs)
```

### Step 3: Assign fit_methods = value

```python
fit_methods = ['LS', 'OLS', 'NNLS', 'RESTORE']
```

### Step 4: Assign dm = dti.TensorModel(...)

```python
dm = dti.TensorModel(gtab)
```

### Step 5: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(dm.fit(100 * np.ones(bvals.shape[0])).fa, 0)
```

### Step 6: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(dm.fit(0.4 * np.ones(bvals.shape[0])).fa, 0)
```


## Complete Example

```python
# Workflow
bvals, bvecs = read_bvals_bvecs(*get_fnames(name='55dir_grad'))
gtab = grad.gradient_table_from_bvals_bvecs(bvals, bvecs)
fit_methods = ['LS', 'OLS', 'NNLS', 'RESTORE']
for _ in fit_methods:
    dm = dti.TensorModel(gtab)
    npt.assert_almost_equal(dm.fit(100 * np.ones(bvals.shape[0])).fa, 0)
    npt.assert_almost_equal(dm.fit(0.4 * np.ones(bvals.shape[0])).fa, 0)
```

## Next Steps


---

*Source: test_dti.py:660 | Complexity: Intermediate | Last updated: 2026-05-18*