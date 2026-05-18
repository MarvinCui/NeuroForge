# How To: Csd Superres

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check the quality of csdfit with high SH order.

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

### Step 1: 'Check the quality of csdfit with high SH order.'

```python
'Check the quality of csdfit with high SH order.'
```

**Verification:**
```python
assert_greater_equal(len(w), 1)
```

### Step 2: Assign unknown = get_fnames(...)

```python
_, fbvals, fbvecs = get_fnames(name='small_64D')
```

**Verification:**
```python
assert_equal(len(d), 2)
```

### Step 3: Assign unknown = read_bvals_bvecs(...)

```python
bvals, bvecs = read_bvals_bvecs(fbvals, fbvecs)
```

**Verification:**
```python
assert_(all(cos_sim > 0.99))
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

### Step 7: Assign fit16 = model16.fit(...)

```python
fit16 = model16.fit(S)
```

### Step 8: Assign sphere = HemiSphere.from_sphere(...)

```python
sphere = HemiSphere.from_sphere(get_sphere(name='symmetric724'))
```

### Step 9: Call assert_equal()

```python
assert_equal(len(d), 2)
```

### Step 10: Assign cos_sim = value

```python
cos_sim = abs((d * sticks).sum(1)) ** 0.5
```

### Step 11: Call assert_()

```python
assert_(all(cos_sim > 0.99))
```

### Step 12: Call warnings.filterwarnings()

```python
warnings.filterwarnings(action='always', message='Number of parameters required.*', category=UserWarning)
```

### Step 13: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 14: Assign model16 = ConstrainedSphericalDeconvModel(...)

```python
model16 = ConstrainedSphericalDeconvModel(gtab, (evals[0], 3.0), sh_order_max=16)
```

### Step 15: Call assert_greater_equal()

```python
assert_greater_equal(len(w), 1)
```

### Step 16: Call npt.assert_()

```python
npt.assert_(issubclass(w[0].category, UserWarning))
```

### Step 17: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 18: Assign unknown = peak_directions(...)

```python
d, v, ind = peak_directions(fit16.odf(sphere), sphere, relative_peak_threshold=0.2, min_separation_angle=0)
```


## Complete Example

```python
# Workflow
'Check the quality of csdfit with high SH order.'
_, fbvals, fbvecs = get_fnames(name='small_64D')
bvals, bvecs = read_bvals_bvecs(fbvals, fbvecs)
gtab = gradient_table(bvals, bvecs=bvecs)
evals = np.array([[1.5, 0.3, 0.3]]) * [[1.0], [1.0]] / 1000.0
S, sticks = multi_tensor(gtab, evals, snr=None, fractions=[55.0, 45.0])
with warnings.catch_warnings(record=True) as w:
    warnings.filterwarnings(action='always', message='Number of parameters required.*', category=UserWarning)
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    model16 = ConstrainedSphericalDeconvModel(gtab, (evals[0], 3.0), sh_order_max=16)
    assert_greater_equal(len(w), 1)
    npt.assert_(issubclass(w[0].category, UserWarning))
fit16 = model16.fit(S)
sphere = HemiSphere.from_sphere(get_sphere(name='symmetric724'))
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    d, v, ind = peak_directions(fit16.odf(sphere), sphere, relative_peak_threshold=0.2, min_separation_angle=0)
assert_equal(len(d), 2)
cos_sim = abs((d * sticks).sum(1)) ** 0.5
assert_(all(cos_sim > 0.99))
```

## Next Steps


---

*Source: test_csdeconv.py:764 | Complexity: Advanced | Last updated: 2026-05-18*