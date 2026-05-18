# How To: Csd Convergence

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check existence of `convergence` keyword in CSD model

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.core.sphere`
- `dipy.core.sphere_stats`
- `dipy.data`
- `dipy.direction.peaks`
- `dipy.io.gradients`
- `dipy.reconst.csdeconv`
- `dipy.reconst.dti`
- `dipy.reconst.shm`
- `dipy.sims.voxel`
- `dipy.testing`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: 'Check existence of `convergence` keyword in CSD model'

```python
'Check existence of `convergence` keyword in CSD model'
```

**Verification:**
```python
assert_equal(model_w_conv.fit(S).shm_coeff, model_wo_conv.fit(S).shm_coeff)
```

### Step 2: Assign unknown = get_fnames(...)

```python
_, fbvals, fbvecs = get_fnames(name='small_64D')
```

### Step 3: Assign unknown = read_bvals_bvecs(...)

```python
bvals, bvecs = read_bvals_bvecs(fbvals, fbvecs)
```

### Step 4: Assign gtab = gradient_table(...)

```python
gtab = gradient_table(bvals, bvecs=bvecs)
```

### Step 5: Assign evals = value

```python
evals = np.array([[1.5, 0.3, 0.3]]) * [[1.0], [1.0]] / 1000.0
```

### Step 6: Assign unknown = multi_tensor(...)

```python
S, sticks = multi_tensor(gtab, evals, snr=None, fractions=[55.0, 45.0])
```

### Step 7: Call assert_equal()

```python
assert_equal(model_w_conv.fit(S).shm_coeff, model_wo_conv.fit(S).shm_coeff)
```

### Step 8: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 9: Assign model_w_conv = ConstrainedSphericalDeconvModel(...)

```python
model_w_conv = ConstrainedSphericalDeconvModel(gtab, (evals[0], 3.0), sh_order_max=8, convergence=50)
```

### Step 10: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 11: Assign model_wo_conv = ConstrainedSphericalDeconvModel(...)

```python
model_wo_conv = ConstrainedSphericalDeconvModel(gtab, (evals[0], 3.0), sh_order_max=8)
```


## Complete Example

```python
# Workflow
'Check existence of `convergence` keyword in CSD model'
_, fbvals, fbvecs = get_fnames(name='small_64D')
bvals, bvecs = read_bvals_bvecs(fbvals, fbvecs)
gtab = gradient_table(bvals, bvecs=bvecs)
evals = np.array([[1.5, 0.3, 0.3]]) * [[1.0], [1.0]] / 1000.0
S, sticks = multi_tensor(gtab, evals, snr=None, fractions=[55.0, 45.0])
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    model_w_conv = ConstrainedSphericalDeconvModel(gtab, (evals[0], 3.0), sh_order_max=8, convergence=50)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    model_wo_conv = ConstrainedSphericalDeconvModel(gtab, (evals[0], 3.0), sh_order_max=8)
assert_equal(model_w_conv.fit(S).shm_coeff, model_wo_conv.fit(S).shm_coeff)
```

## Next Steps


---

*Source: test_csdeconv.py:816 | Complexity: Advanced | Last updated: 2026-05-18*