# How To: Fit Data

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test fit data

## Prerequisites

**Required Modules:**
- `os.path`
- `nibabel`
- `numpy`
- `numpy.testing`
- `scipy.linalg`
- `dipy.core.gradients`
- `dipy.core.optimize`
- `dipy.data`
- `dipy.io.gradients`
- `dipy.io.image`
- `dipy.io.stateful_tractogram`
- `dipy.tracking.life`


## Step-by-Step Guide

### Step 1: Assign unknown = dpd.get_fnames(...)

```python
fdata, fbval, fbvec = dpd.get_fnames(name='small_25')
```

### Step 2: Assign fstreamlines = dpd.get_fnames(...)

```python
fstreamlines = dpd.get_fnames(name='small_25_streamlines')
```

### Step 3: Assign gtab = grad.gradient_table(...)

```python
gtab = grad.gradient_table(fbval, bvecs=fbvec)
```

### Step 4: Assign ni_data = nib.load(...)

```python
ni_data = nib.load(fdata)
```

### Step 5: Assign data = np.asarray(...)

```python
data = np.asarray(ni_data.dataobj)
```

### Step 6: Assign tensor_streamlines = value

```python
tensor_streamlines = nib.streamlines.load(fstreamlines).streamlines
```

### Step 7: Assign sft = StatefulTractogram(...)

```python
sft = StatefulTractogram(tensor_streamlines, ni_data, Space.RASMM)
```

### Step 8: Call sft.to_vox()

```python
sft.to_vox()
```

### Step 9: Assign tensor_streamlines_vox = value

```python
tensor_streamlines_vox = sft.streamlines
```

### Step 10: Assign life_model = life.FiberModel(...)

```python
life_model = life.FiberModel(gtab)
```

### Step 11: Assign life_fit = life_model.fit(...)

```python
life_fit = life_model.fit(data, tensor_streamlines_vox, np.eye(4))
```

### Step 12: Assign model_error = value

```python
model_error = life_fit.predict() - life_fit.data
```

### Step 13: Assign model_rmse = np.sqrt(...)

```python
model_rmse = np.sqrt(np.mean(model_error ** 2, -1))
```

### Step 14: Assign unknown = dpd.matlab_life_results(...)

```python
matlab_rmse, matlab_weights = dpd.matlab_life_results()
```

### Step 15: Call npt.assert_()

```python
npt.assert_(np.median(model_rmse) < np.median(matlab_rmse))
```

### Step 16: Call npt.assert_()

```python
npt.assert_(np.corrcoef(matlab_weights, life_fit.beta)[0, 1] > 0.6)
```


## Complete Example

```python
# Workflow
fdata, fbval, fbvec = dpd.get_fnames(name='small_25')
fstreamlines = dpd.get_fnames(name='small_25_streamlines')
gtab = grad.gradient_table(fbval, bvecs=fbvec)
ni_data = nib.load(fdata)
data = np.asarray(ni_data.dataobj)
tensor_streamlines = nib.streamlines.load(fstreamlines).streamlines
sft = StatefulTractogram(tensor_streamlines, ni_data, Space.RASMM)
sft.to_vox()
tensor_streamlines_vox = sft.streamlines
life_model = life.FiberModel(gtab)
life_fit = life_model.fit(data, tensor_streamlines_vox, np.eye(4))
model_error = life_fit.predict() - life_fit.data
model_rmse = np.sqrt(np.mean(model_error ** 2, -1))
matlab_rmse, matlab_weights = dpd.matlab_life_results()
npt.assert_(np.median(model_rmse) < np.median(matlab_rmse))
npt.assert_(np.corrcoef(matlab_weights, life_fit.beta)[0, 1] > 0.6)
```

## Next Steps


---

*Source: test_life.py:165 | Complexity: Advanced | Last updated: 2026-05-18*