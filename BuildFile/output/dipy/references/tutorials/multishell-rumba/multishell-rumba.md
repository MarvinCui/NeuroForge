# How To: Multishell Rumba

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test multishell rumba

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
assert_equal(len(directions), 2)
```

### Step 2: Assign btable = np.loadtxt(...)

```python
btable = np.loadtxt(get_fnames(name='dsi515btable'))
```

**Verification:**
```python
assert_almost_equal(angular_similarity(directions, golden_directions), 2, 1)
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

### Step 6: Assign unknown = sticks_and_ball(...)

```python
data, golden_directions = sticks_and_ball(gtab, d=0.0015, S0=100, angles=[(0, 0), (90, 0)], fractions=[50, 50], snr=None)
```

### Step 7: Assign ms_eigenval_count = value

```python
ms_eigenval_count = len(unique_bvals_tolerance(gtab.bvals)) - 1
```

### Step 8: Assign wm_response = np.tile(...)

```python
wm_response = np.tile(np.array([0.0017, 0.0002, 0.0002]), (ms_eigenval_count, 1))
```

### Step 9: Assign model = RumbaSDModel(...)

```python
model = RumbaSDModel(gtab, wm_response=wm_response, n_iter=20, sphere=sphere)
```

### Step 10: Assign model_fit = model.fit(...)

```python
model_fit = model.fit(data)
```

### Step 11: Assign odf = model_fit.odf(...)

```python
odf = model_fit.odf(sphere=sphere)
```

### Step 12: Assign unknown = peak_directions(...)

```python
directions, _, _ = peak_directions(odf, sphere, relative_peak_threshold=0.35, min_separation_angle=25)
```

### Step 13: Call assert_equal()

```python
assert_equal(len(directions), 2)
```

### Step 14: Call assert_almost_equal()

```python
assert_almost_equal(angular_similarity(directions, golden_directions), 2, 1)
```


## Complete Example

```python
# Workflow
sphere = default_sphere
btable = np.loadtxt(get_fnames(name='dsi515btable'))
bvals = btable[:, 0]
bvecs = btable[:, 1:]
gtab = gradient_table(bvals, bvecs=bvecs)
data, golden_directions = sticks_and_ball(gtab, d=0.0015, S0=100, angles=[(0, 0), (90, 0)], fractions=[50, 50], snr=None)
ms_eigenval_count = len(unique_bvals_tolerance(gtab.bvals)) - 1
wm_response = np.tile(np.array([0.0017, 0.0002, 0.0002]), (ms_eigenval_count, 1))
model = RumbaSDModel(gtab, wm_response=wm_response, n_iter=20, sphere=sphere)
model_fit = model.fit(data)
odf = model_fit.odf(sphere=sphere)
directions, _, _ = peak_directions(odf, sphere, relative_peak_threshold=0.35, min_separation_angle=25)
assert_equal(len(directions), 2)
assert_almost_equal(angular_similarity(directions, golden_directions), 2, 1)
```

## Next Steps


---

*Source: test_rumba.py:154 | Complexity: Advanced | Last updated: 2026-05-18*