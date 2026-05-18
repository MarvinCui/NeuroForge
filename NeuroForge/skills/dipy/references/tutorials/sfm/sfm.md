# How To: Sfm

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test sfm

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

### Step 4: Assign sfmodel = sfm.SparseFascicleModel(...)

```python
sfmodel = sfm.SparseFascicleModel(gtab, isotropic=iso)
```

### Step 5: Assign sffit1 = sfmodel.fit(...)

```python
sffit1 = sfmodel.fit(data[0, 0, 0], num_processes=n_procs)
```

### Step 6: Assign sphere = dpd.get_sphere(...)

```python
sphere = dpd.get_sphere()
```

### Step 7: Assign odf1 = sffit1.odf(...)

```python
odf1 = sffit1.odf(sphere)
```

### Step 8: Assign pred1 = sffit1.predict(...)

```python
pred1 = sffit1.predict(gtab=gtab)
```

### Step 9: Assign mask = np.ones(...)

```python
mask = np.ones(data.shape[:-1])
```

### Step 10: Assign sffit2 = sfmodel.fit(...)

```python
sffit2 = sfmodel.fit(data, mask=mask, num_processes=n_procs)
```

### Step 11: Assign pred2 = sffit2.predict(...)

```python
pred2 = sffit2.predict(gtab=gtab)
```

### Step 12: Assign odf2 = sffit2.odf(...)

```python
odf2 = sffit2.odf(sphere)
```

### Step 13: Assign sffit3 = sfmodel.fit(...)

```python
sffit3 = sfmodel.fit(data, num_processes=n_procs)
```

### Step 14: Assign pred3 = sffit3.predict(...)

```python
pred3 = sffit3.predict(gtab=gtab)
```

### Step 15: Assign odf3 = sffit3.odf(...)

```python
odf3 = sffit3.odf(sphere)
```

### Step 16: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(pred3, pred2, decimal=2)
```

### Step 17: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(pred3[0, 0, 0], pred1, decimal=2)
```

### Step 18: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(odf3[0, 0, 0], odf1, decimal=2)
```

### Step 19: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(odf3[0, 0, 0], odf2[0, 0, 0], decimal=2)
```

### Step 20: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(sfmodel.fit(np.zeros(data[0, 0, 0].shape), num_processes=n_procs).beta, np.zeros(sfmodel.design_matrix[0].shape[-1]))
```


## Complete Example

```python
# Workflow
fdata, fbvals, fbvecs = dpd.get_fnames()
data = load_nifti_data(fdata)
gtab = grad.gradient_table(fbvals, bvecs=fbvecs)
for n_procs in [1, 2]:
    for iso in [sfm.ExponentialIsotropicModel, None]:
        sfmodel = sfm.SparseFascicleModel(gtab, isotropic=iso)
        sffit1 = sfmodel.fit(data[0, 0, 0], num_processes=n_procs)
        sphere = dpd.get_sphere()
        odf1 = sffit1.odf(sphere)
        pred1 = sffit1.predict(gtab=gtab)
        mask = np.ones(data.shape[:-1])
        sffit2 = sfmodel.fit(data, mask=mask, num_processes=n_procs)
        pred2 = sffit2.predict(gtab=gtab)
        odf2 = sffit2.odf(sphere)
        sffit3 = sfmodel.fit(data, num_processes=n_procs)
        pred3 = sffit3.predict(gtab=gtab)
        odf3 = sffit3.odf(sphere)
        npt.assert_almost_equal(pred3, pred2, decimal=2)
        npt.assert_almost_equal(pred3[0, 0, 0], pred1, decimal=2)
        npt.assert_almost_equal(odf3[0, 0, 0], odf1, decimal=2)
        npt.assert_almost_equal(odf3[0, 0, 0], odf2[0, 0, 0], decimal=2)
        npt.assert_almost_equal(sfmodel.fit(np.zeros(data[0, 0, 0].shape), num_processes=n_procs).beta, np.zeros(sfmodel.design_matrix[0].shape[-1]))
```

## Next Steps


---

*Source: test_sfm.py:35 | Complexity: Advanced | Last updated: 2026-05-18*