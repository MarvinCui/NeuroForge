# How To: Diffusivities

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test diffusivities

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

### Step 1: Assign psphere = get_sphere(...)

```python
psphere = get_sphere(name='symmetric362')
```

### Step 2: Assign bvecs = np.concatenate(...)

```python
bvecs = np.concatenate(([[0, 0, 0]], psphere.vertices))
```

### Step 3: Assign bvals = value

```python
bvals = np.zeros(len(bvecs)) + 1000
```

### Step 4: Assign unknown = 0

```python
bvals[0] = 0
```

### Step 5: Assign gtab = grad.gradient_table(...)

```python
gtab = grad.gradient_table(bvals, bvecs=bvecs)
```

### Step 6: Assign mevals = np.array(...)

```python
mevals = np.array(([0.0015, 0.0003, 0.0001], [0.0015, 0.0003, 0.0003]))
```

### Step 7: Assign mevecs = value

```python
mevecs = [np.array([[1, 0, 0], [0, 1, 0], [0, 0, 1]]), np.array([[0, 0, 1], [0, 1, 0], [1, 0, 0]])]
```

### Step 8: Assign S = single_tensor(...)

```python
S = single_tensor(gtab, 100, evals=mevals[0], evecs=mevecs[0], snr=None)
```

### Step 9: Assign dm = dti.TensorModel(...)

```python
dm = dti.TensorModel(gtab, fit_method='LS')
```

### Step 10: Assign dmfit = dm.fit(...)

```python
dmfit = dm.fit(S)
```

### Step 11: Assign md = mean_diffusivity(...)

```python
md = mean_diffusivity(dmfit.evals)
```

### Step 12: Assign Trace = trace(...)

```python
Trace = trace(dmfit.evals)
```

### Step 13: Assign rd = radial_diffusivity(...)

```python
rd = radial_diffusivity(dmfit.evals)
```

### Step 14: Assign ad = axial_diffusivity(...)

```python
ad = axial_diffusivity(dmfit.evals)
```

### Step 15: Assign lin = linearity(...)

```python
lin = linearity(dmfit.evals)
```

### Step 16: Assign plan = planarity(...)

```python
plan = planarity(dmfit.evals)
```

### Step 17: Assign spher = sphericity(...)

```python
spher = sphericity(dmfit.evals)
```

### Step 18: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(md, (0.0015 + 0.0003 + 0.0001) / 3)
```

### Step 19: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(Trace, 0.0015 + 0.0003 + 0.0001)
```

### Step 20: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(ad, 0.0015)
```

### Step 21: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(rd, (0.0003 + 0.0001) / 2)
```

### Step 22: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(lin, (0.0015 - 0.0003) / Trace)
```

### Step 23: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(plan, 2 * (0.0003 - 0.0001) / Trace)
```

### Step 24: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(spher, 3 * 0.0001 / Trace)
```


## Complete Example

```python
# Workflow
psphere = get_sphere(name='symmetric362')
bvecs = np.concatenate(([[0, 0, 0]], psphere.vertices))
bvals = np.zeros(len(bvecs)) + 1000
bvals[0] = 0
gtab = grad.gradient_table(bvals, bvecs=bvecs)
mevals = np.array(([0.0015, 0.0003, 0.0001], [0.0015, 0.0003, 0.0003]))
mevecs = [np.array([[1, 0, 0], [0, 1, 0], [0, 0, 1]]), np.array([[0, 0, 1], [0, 1, 0], [1, 0, 0]])]
S = single_tensor(gtab, 100, evals=mevals[0], evecs=mevecs[0], snr=None)
dm = dti.TensorModel(gtab, fit_method='LS')
dmfit = dm.fit(S)
md = mean_diffusivity(dmfit.evals)
Trace = trace(dmfit.evals)
rd = radial_diffusivity(dmfit.evals)
ad = axial_diffusivity(dmfit.evals)
lin = linearity(dmfit.evals)
plan = planarity(dmfit.evals)
spher = sphericity(dmfit.evals)
npt.assert_almost_equal(md, (0.0015 + 0.0003 + 0.0001) / 3)
npt.assert_almost_equal(Trace, 0.0015 + 0.0003 + 0.0001)
npt.assert_almost_equal(ad, 0.0015)
npt.assert_almost_equal(rd, (0.0003 + 0.0001) / 2)
npt.assert_almost_equal(lin, (0.0015 - 0.0003) / Trace)
npt.assert_almost_equal(plan, 2 * (0.0003 - 0.0001) / Trace)
npt.assert_almost_equal(spher, 3 * 0.0001 / Trace)
```

## Next Steps


---

*Source: test_dti.py:277 | Complexity: Advanced | Last updated: 2026-05-18*