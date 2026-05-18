# How To: Odf With Zeros

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test odf with zeros

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

### Step 1: Assign unknown = get_fnames(...)

```python
fdata, fbval, fbvec = get_fnames(name='small_25')
```

### Step 2: Assign gtab = grad.gradient_table(...)

```python
gtab = grad.gradient_table(fbval, bvecs=fbvec)
```

### Step 3: Assign data = load_nifti_data(...)

```python
data = load_nifti_data(fdata)
```

### Step 4: Assign dm = dti.TensorModel(...)

```python
dm = dti.TensorModel(gtab)
```

### Step 5: Assign df = dm.fit(...)

```python
df = dm.fit(data)
```

### Step 6: Assign unknown = np.array(...)

```python
df.evals[0, 0, 0] = np.array([0, 0, 0])
```

### Step 7: Assign sphere = create_unit_sphere(...)

```python
sphere = create_unit_sphere(recursion_level=4)
```

### Step 8: Assign odf = df.odf(...)

```python
odf = df.odf(sphere)
```

### Step 9: Call npt.assert_equal()

```python
npt.assert_equal(odf[0, 0, 0], np.zeros(sphere.vertices.shape[0]))
```


## Complete Example

```python
# Workflow
fdata, fbval, fbvec = get_fnames(name='small_25')
gtab = grad.gradient_table(fbval, bvecs=fbvec)
data = load_nifti_data(fdata)
dm = dti.TensorModel(gtab)
df = dm.fit(data)
df.evals[0, 0, 0] = np.array([0, 0, 0])
sphere = create_unit_sphere(recursion_level=4)
odf = df.odf(sphere)
npt.assert_equal(odf[0, 0, 0], np.zeros(sphere.vertices.shape[0]))
```

## Next Steps


---

*Source: test_dti.py:67 | Complexity: Advanced | Last updated: 2026-05-18*