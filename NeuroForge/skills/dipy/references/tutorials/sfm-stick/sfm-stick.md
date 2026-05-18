# How To: Sfm Stick

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test sfm stick

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
sfmodel = sfm.SparseFascicleModel(gtab, solver='NNLS', response=[0.001, 0, 0])
```

### Step 5: Assign sffit1 = sfmodel.fit(...)

```python
sffit1 = sfmodel.fit(data[0, 0, 0])
```

### Step 6: Assign sphere = dpd.get_sphere(...)

```python
sphere = dpd.get_sphere()
```

### Step 7: Call sffit1.odf()

```python
sffit1.odf(sphere)
```

### Step 8: Call sffit1.predict()

```python
sffit1.predict(gtab=gtab)
```

### Step 9: Assign SNR = 1000

```python
SNR = 1000
```

### Step 10: Assign S0 = 100

```python
S0 = 100
```

### Step 11: Assign mevals = np.array(...)

```python
mevals = np.array(([0.001, 0, 0], [0.001, 0, 0]))
```

### Step 12: Assign angles = value

```python
angles = [(0, 0), (60, 0)]
```

### Step 13: Assign unknown = sims.multi_tensor(...)

```python
S, sticks = sims.multi_tensor(gtab, mevals, S0=S0, angles=angles, fractions=[50, 50], snr=SNR)
```

### Step 14: Assign sfmodel = sfm.SparseFascicleModel(...)

```python
sfmodel = sfm.SparseFascicleModel(gtab, solver='NNLS', response=[0.001, 0, 0])
```

### Step 15: Assign sffit = sfmodel.fit(...)

```python
sffit = sfmodel.fit(S)
```

### Step 16: Assign pred = sffit.predict(...)

```python
pred = sffit.predict()
```

### Step 17: Call npt.assert_()

```python
npt.assert_(xval.coeff_of_determination(pred, S) > 96)
```


## Complete Example

```python
# Workflow
fdata, fbvals, fbvecs = dpd.get_fnames()
data = load_nifti_data(fdata)
gtab = grad.gradient_table(fbvals, bvecs=fbvecs)
sfmodel = sfm.SparseFascicleModel(gtab, solver='NNLS', response=[0.001, 0, 0])
sffit1 = sfmodel.fit(data[0, 0, 0])
sphere = dpd.get_sphere()
sffit1.odf(sphere)
sffit1.predict(gtab=gtab)
SNR = 1000
S0 = 100
mevals = np.array(([0.001, 0, 0], [0.001, 0, 0]))
angles = [(0, 0), (60, 0)]
S, sticks = sims.multi_tensor(gtab, mevals, S0=S0, angles=angles, fractions=[50, 50], snr=SNR)
sfmodel = sfm.SparseFascicleModel(gtab, solver='NNLS', response=[0.001, 0, 0])
sffit = sfmodel.fit(S)
pred = sffit.predict()
npt.assert_(xval.coeff_of_determination(pred, S) > 96)
```

## Next Steps


---

*Source: test_sfm.py:152 | Complexity: Advanced | Last updated: 2026-05-18*