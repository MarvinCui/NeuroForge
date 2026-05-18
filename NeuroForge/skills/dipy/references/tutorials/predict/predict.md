# How To: Predict

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test predict

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `dipy.core.geometry`
- `dipy.core.gradients`
- `dipy.core.sphere_stats`
- `dipy.data`
- `dipy.direction.peaks`
- `dipy.reconst.csdeconv`
- `dipy.reconst.rumba`
- `dipy.reconst.shm`
- `dipy.reconst.tests.test_dsi`
- `dipy.sims.voxel`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign sphere = default_sphere

```python
sphere = default_sphere
```

**Verification:**
```python
assert_allclose(data_pred, data, atol=0.01, rtol=0.05)
```

### Step 2: Assign btable = np.loadtxt(...)

```python
btable = np.loadtxt(get_fnames(name='dsi515btable'))
```

### Step 3: Assign bvals = value

```python
bvals = btable[:, 0]
```

### Step 4: Assign bvecs = value

```python
bvecs = btable[:, 1:]
```

### Step 5: Assign gtab = gradient_table(...)

```python
gtab = gradient_table(bvals, bvecs=bvecs)
```

### Step 6: Assign rumba = RumbaSDModel(...)

```python
rumba = RumbaSDModel(gtab, n_iter=600, sphere=sphere)
```

### Step 7: Assign data = single_tensor(...)

```python
data = single_tensor(gtab, S0=1, evals=rumba.wm_response)
```

### Step 8: Assign rumba_fit = rumba.fit(...)

```python
rumba_fit = rumba.fit(data)
```

### Step 9: Assign data_pred = rumba_fit.predict(...)

```python
data_pred = rumba_fit.predict()
```

### Step 10: Call assert_allclose()

```python
assert_allclose(data_pred, data, atol=0.01, rtol=0.05)
```


## Complete Example

```python
# Workflow
sphere = default_sphere
btable = np.loadtxt(get_fnames(name='dsi515btable'))
bvals = btable[:, 0]
bvecs = btable[:, 1:]
gtab = gradient_table(bvals, bvecs=bvecs)
rumba = RumbaSDModel(gtab, n_iter=600, sphere=sphere)
data = single_tensor(gtab, S0=1, evals=rumba.wm_response)
rumba_fit = rumba.fit(data)
data_pred = rumba_fit.predict()
assert_allclose(data_pred, data, atol=0.01, rtol=0.05)
```

## Next Steps


---

*Source: test_rumba.py:99 | Complexity: Advanced | Last updated: 2026-05-18*