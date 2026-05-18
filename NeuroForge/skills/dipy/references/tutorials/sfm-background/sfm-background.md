# How To: Sfm Background

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test sfm background

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.core.gradients`
- `dipy.core.optimize`
- `dipy.data`
- `dipy.io.gradients`
- `dipy.io.image`
- `dipy.reconst.cross_validation`
- `dipy.reconst.sfm`
- `dipy.sims.voxel`
- `dipy.utils.optpkg`


## Step-by-Step Guide

### Step 1: Assign unknown = dpd.get_fnames(...)

```python
fdata, fbvals, fbvecs = dpd.get_fnames()
```

### Step 2: Assign data = load_nifti_data(...)

```python
data = load_nifti_data(fdata)
```

### Step 3: Assign gtab = grad.gradient_table(...)

```python
gtab = grad.gradient_table(fbvals, bvecs=fbvecs)
```

### Step 4: Assign to_fit = value

```python
to_fit = data[0, 0, 0]
```

### Step 5: Assign unknown = 0

```python
to_fit[gtab.b0s_mask] = 0
```

### Step 6: Assign sfmodel = sfm.SparseFascicleModel(...)

```python
sfmodel = sfm.SparseFascicleModel(gtab, solver='NNLS')
```

### Step 7: Assign sffit = sfmodel.fit(...)

```python
sffit = sfmodel.fit(to_fit)
```

### Step 8: Call npt.assert_equal()

```python
npt.assert_equal(sffit.beta, np.zeros_like(sffit.beta))
```


## Complete Example

```python
# Workflow
fdata, fbvals, fbvecs = dpd.get_fnames()
data = load_nifti_data(fdata)
gtab = grad.gradient_table(fbvals, bvecs=fbvecs)
to_fit = data[0, 0, 0]
to_fit[gtab.b0s_mask] = 0
sfmodel = sfm.SparseFascicleModel(gtab, solver='NNLS')
sffit = sfmodel.fit(to_fit)
npt.assert_equal(sffit.beta, np.zeros_like(sffit.beta))
```

## Next Steps


---

*Source: test_sfm.py:141 | Complexity: Advanced | Last updated: 2026-05-18*