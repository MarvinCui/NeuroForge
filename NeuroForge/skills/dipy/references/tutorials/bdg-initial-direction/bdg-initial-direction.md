# How To: Bdg Initial Direction

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: This tests the number of initial directions." 

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `dipy.core.geometry`
- `dipy.core.gradients`
- `dipy.core.sphere`
- `dipy.data`
- `dipy.direction.bootstrap_direction_getter`
- `dipy.io.gradients`
- `dipy.reconst`
- `dipy.reconst.csdeconv`
- `dipy.sims.voxel`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: 'This tests the number of initial directions." '

```python
'This tests the number of initial directions." '
```

### Step 2: Assign hsph_updated = HemiSphere.from_sphere.subdivide(...)

```python
hsph_updated = HemiSphere.from_sphere(unit_icosahedron).subdivide(n=2)
```

### Step 3: Assign vertices = value

```python
vertices = hsph_updated.vertices
```

### Step 4: Assign bvecs = vertices

```python
bvecs = vertices
```

### Step 5: Assign bvals = value

```python
bvals = np.ones(len(vertices)) * 1000
```

### Step 6: Assign bvecs = np.insert(...)

```python
bvecs = np.insert(bvecs, 0, np.array([0, 0, 0]), axis=0)
```

### Step 7: Assign bvals = np.insert(...)

```python
bvals = np.insert(bvals, 0, 0)
```

### Step 8: Assign gtab = gradient_table(...)

```python
gtab = gradient_table(bvals, bvecs=bvecs)
```

### Step 9: Assign sphere = HemiSphere.from_sphere(...)

```python
sphere = HemiSphere.from_sphere(get_sphere(name='symmetric724'))
```

### Step 10: Assign voxel = single_tensor.reshape(...)

```python
voxel = single_tensor(gtab).reshape([1, 1, 1, -1])
```

### Step 11: Assign dti_model = dti.TensorModel(...)

```python
dti_model = dti.TensorModel(gtab)
```

### Step 12: Assign initial_direction = boot_dg.initial_direction(...)

```python
initial_direction = boot_dg.initial_direction(np.zeros(3))
```

### Step 13: Call npt.assert_equal()

```python
npt.assert_equal(len(initial_direction), 1)
```

### Step 14: Call npt.assert_allclose()

```python
npt.assert_allclose(initial_direction[0], [1, 0, 0], atol=0.1)
```

### Step 15: Assign mevals = value

```python
mevals = np.array([[1.5, 0.4, 0.4], [1.5, 0.4, 0.4]]) * 0.001
```

### Step 16: Assign fracs = value

```python
fracs = [60, 40]
```

### Step 17: Assign unknown = multi_tensor(...)

```python
voxel, primary_evecs = multi_tensor(gtab, mevals, fractions=fracs, snr=None)
```

### Step 18: Assign voxel = voxel.reshape(...)

```python
voxel = voxel.reshape([1, 1, 1, -1])
```

### Step 19: Assign response = value

```python
response = (np.array([0.0015, 0.0004, 0.0004]), 1)
```

### Step 20: Call npt.assert_equal()

```python
npt.assert_equal(len(initial_direction), 2)
```

### Step 21: Call npt.assert_allclose()

```python
npt.assert_allclose(initial_direction, primary_evecs, atol=0.1)
```

### Step 22: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 23: Assign boot_dg = BootDirectionGetter.from_data(...)

```python
boot_dg = BootDirectionGetter.from_data(voxel, dti_model, 30, sphere=sphere, sh_order=6)
```

### Step 24: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 25: Assign csd_model = ConstrainedSphericalDeconvModel(...)

```python
csd_model = ConstrainedSphericalDeconvModel(gtab, response=response, sh_order_max=4)
```

### Step 26: Assign boot_dg = BootDirectionGetter.from_data(...)

```python
boot_dg = BootDirectionGetter.from_data(voxel, csd_model, 30, sphere=sphere)
```

### Step 27: Assign initial_direction = boot_dg.initial_direction(...)

```python
initial_direction = boot_dg.initial_direction(np.zeros(3))
```


## Complete Example

```python
# Workflow
'This tests the number of initial directions." '
hsph_updated = HemiSphere.from_sphere(unit_icosahedron).subdivide(n=2)
vertices = hsph_updated.vertices
bvecs = vertices
bvals = np.ones(len(vertices)) * 1000
bvecs = np.insert(bvecs, 0, np.array([0, 0, 0]), axis=0)
bvals = np.insert(bvals, 0, 0)
gtab = gradient_table(bvals, bvecs=bvecs)
sphere = HemiSphere.from_sphere(get_sphere(name='symmetric724'))
voxel = single_tensor(gtab).reshape([1, 1, 1, -1])
dti_model = dti.TensorModel(gtab)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    boot_dg = BootDirectionGetter.from_data(voxel, dti_model, 30, sphere=sphere, sh_order=6)
initial_direction = boot_dg.initial_direction(np.zeros(3))
npt.assert_equal(len(initial_direction), 1)
npt.assert_allclose(initial_direction[0], [1, 0, 0], atol=0.1)
mevals = np.array([[1.5, 0.4, 0.4], [1.5, 0.4, 0.4]]) * 0.001
fracs = [60, 40]
voxel, primary_evecs = multi_tensor(gtab, mevals, fractions=fracs, snr=None)
voxel = voxel.reshape([1, 1, 1, -1])
response = (np.array([0.0015, 0.0004, 0.0004]), 1)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=shm.descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    csd_model = ConstrainedSphericalDeconvModel(gtab, response=response, sh_order_max=4)
    boot_dg = BootDirectionGetter.from_data(voxel, csd_model, 30, sphere=sphere)
    initial_direction = boot_dg.initial_direction(np.zeros(3))
npt.assert_equal(len(initial_direction), 2)
npt.assert_allclose(initial_direction, primary_evecs, atol=0.1)
```

## Next Steps


---

*Source: test_bootstrap_direction_getter.py:18 | Complexity: Advanced | Last updated: 2026-05-18*