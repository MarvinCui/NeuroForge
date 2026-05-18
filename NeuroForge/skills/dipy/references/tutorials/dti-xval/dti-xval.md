# How To: Dti Xval

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test dti xval

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.data`
- `dipy.io.image`
- `dipy.reconst.base`
- `dipy.reconst.cross_validation`
- `dipy.reconst.csdeconv`
- `dipy.reconst.dti`
- `dipy.reconst.shm`
- `dipy.sims.voxel`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign data = load_nifti_data(...)

```python
data = load_nifti_data(fdata)
```

### Step 2: Assign gtab = gt.gradient_table(...)

```python
gtab = gt.gradient_table(fbval, bvecs=fbvec)
```

### Step 3: Assign dm = dti.TensorModel(...)

```python
dm = dti.TensorModel(gtab, fit_method='LS')
```

### Step 4: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, xval.kfold_xval, dm, data, 10)
```

### Step 5: Assign psphere = dpd.get_sphere(...)

```python
psphere = dpd.get_sphere(name='symmetric362')
```

### Step 6: Assign bvecs = np.concatenate(...)

```python
bvecs = np.concatenate(([[0, 0, 0]], psphere.vertices))
```

### Step 7: Assign bvals = value

```python
bvals = np.zeros(len(bvecs)) + 1000
```

### Step 8: Assign unknown = 0

```python
bvals[0] = 0
```

### Step 9: Assign gtab = gt.gradient_table(...)

```python
gtab = gt.gradient_table(bvals, bvecs=bvecs)
```

### Step 10: Assign mevals = np.array(...)

```python
mevals = np.array(([0.0015, 0.0003, 0.0001], [0.0015, 0.0003, 0.0003]))
```

### Step 11: Assign mevecs = value

```python
mevecs = [np.array([[1, 0, 0], [0, 1, 0], [0, 0, 1]]), np.array([[0, 0, 1], [0, 1, 0], [1, 0, 0]])]
```

### Step 12: Assign S = sims.single_tensor(...)

```python
S = sims.single_tensor(gtab, 100, evals=mevals[0], evecs=mevecs[0], snr=None)
```

### Step 13: Assign dm = dti.TensorModel(...)

```python
dm = dti.TensorModel(gtab, fit_method='LS')
```

### Step 14: Assign kf_xval = xval.kfold_xval(...)

```python
kf_xval = xval.kfold_xval(dm, S, 2)
```

### Step 15: Assign cod = xval.coeff_of_determination(...)

```python
cod = xval.coeff_of_determination(S, kf_xval)
```

### Step 16: Call npt.assert_array_almost_equal()

```python
npt.assert_array_almost_equal(cod, np.ones(kf_xval.shape[:-1]) * 100)
```

### Step 17: Assign S = np.array(...)

```python
S = np.array([[S, S], [S, S]])
```

### Step 18: Assign mask = np.ones(...)

```python
mask = np.ones(S.shape[:-1], dtype=bool)
```

### Step 19: Assign unknown = 0

```python
mask[1, 1] = 0
```

### Step 20: Assign kf_xval = xval.kfold_xval(...)

```python
kf_xval = xval.kfold_xval(dm, S, 2, mask=mask)
```

### Step 21: Assign cod2d = xval.coeff_of_determination(...)

```python
cod2d = xval.coeff_of_determination(S, kf_xval)
```

### Step 22: Call npt.assert_array_almost_equal()

```python
npt.assert_array_almost_equal(np.round(cod2d[0, 0]), cod)
```


## Complete Example

```python
# Workflow
data = load_nifti_data(fdata)
gtab = gt.gradient_table(fbval, bvecs=fbvec)
dm = dti.TensorModel(gtab, fit_method='LS')
npt.assert_raises(ValueError, xval.kfold_xval, dm, data, 10)
psphere = dpd.get_sphere(name='symmetric362')
bvecs = np.concatenate(([[0, 0, 0]], psphere.vertices))
bvals = np.zeros(len(bvecs)) + 1000
bvals[0] = 0
gtab = gt.gradient_table(bvals, bvecs=bvecs)
mevals = np.array(([0.0015, 0.0003, 0.0001], [0.0015, 0.0003, 0.0003]))
mevecs = [np.array([[1, 0, 0], [0, 1, 0], [0, 0, 1]]), np.array([[0, 0, 1], [0, 1, 0], [1, 0, 0]])]
S = sims.single_tensor(gtab, 100, evals=mevals[0], evecs=mevecs[0], snr=None)
dm = dti.TensorModel(gtab, fit_method='LS')
kf_xval = xval.kfold_xval(dm, S, 2)
cod = xval.coeff_of_determination(S, kf_xval)
npt.assert_array_almost_equal(cod, np.ones(kf_xval.shape[:-1]) * 100)
S = np.array([[S, S], [S, S]])
mask = np.ones(S.shape[:-1], dtype=bool)
mask[1, 1] = 0
kf_xval = xval.kfold_xval(dm, S, 2, mask=mask)
cod2d = xval.coeff_of_determination(S, kf_xval)
npt.assert_array_almost_equal(np.round(cod2d[0, 0]), cod)
```

## Next Steps


---

*Source: test_cross_validation.py:32 | Complexity: Advanced | Last updated: 2026-05-18*