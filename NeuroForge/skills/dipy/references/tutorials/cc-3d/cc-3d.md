# How To: Cc 3D

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test 3D SyN with CC metric

Register a volume created by stacking copies of a coronal slice from
a T1w brain MRI before and after warping it under a synthetic
invertible map. We verify that the final registration is of good
quality.

## Prerequisites

**Required Modules:**
- `nibabel.eulerangles`
- `numpy`
- `numpy.testing`
- `dipy.align`
- `dipy.align.imwarp`
- `dipy.core.interpolation`
- `dipy.data`
- `dipy.testing.decorators`
- `dipy.tracking.streamline`


## Step-by-Step Guide

### Step 1: 'Test 3D SyN with CC metric\n\n    Register a volume created by stacking copies of a coronal slice from\n    a T1w brain MRI before and after warping it under a synthetic\n    invertible map. We verify that the final registration is of good\n    quality.\n    '

```python
'Test 3D SyN with CC metric\n\n    Register a volume created by stacking copies of a coronal slice from\n    a T1w brain MRI before and after warping it under a synthetic\n    invertible map. We verify that the final registration is of good\n    quality.\n    '
```

**Verification:**
```python
assert_equal(mapping, m)
```

### Step 2: Assign fname = get_fnames(...)

```python
fname = get_fnames(name='t1_coronal_slice')
```

**Verification:**
```python
assert_equal(s2ref, optimizer.static_to_ref)
```

### Step 3: Assign nslices = 21

```python
nslices = 21
```

**Verification:**
```python
assert_equal(m2ref, optimizer.moving_to_ref)
```

### Step 4: Assign b = 0.1

```python
b = 0.1
```

**Verification:**
```python
assert reduced > 0.9
```

### Step 5: Assign m = 4

```python
m = 4
```

### Step 6: Assign image = np.load(...)

```python
image = np.load(fname)
```

### Step 7: Assign unknown = get_warped_stacked_image(...)

```python
moving, static = get_warped_stacked_image(image, nslices, b, m)
```

### Step 8: Assign sigma_diff = 2.0

```python
sigma_diff = 2.0
```

### Step 9: Assign radius = 2

```python
radius = 2
```

### Step 10: Assign similarity_metric = metrics.CCMetric(...)

```python
similarity_metric = metrics.CCMetric(3, sigma_diff=sigma_diff, radius=radius)
```

### Step 11: Assign level_iters = value

```python
level_iters = [20, 5]
```

### Step 12: Assign step_length = 0.25

```python
step_length = 0.25
```

### Step 13: Assign opt_tol = 0.0001

```python
opt_tol = 0.0001
```

### Step 14: Assign inv_iter = 20

```python
inv_iter = 20
```

### Step 15: Assign inv_tol = 0.001

```python
inv_tol = 0.001
```

### Step 16: Assign ss_sigma_factor = 0.2

```python
ss_sigma_factor = 0.2
```

### Step 17: Assign optimizer = imwarp.SymmetricDiffeomorphicRegistration(...)

```python
optimizer = imwarp.SymmetricDiffeomorphicRegistration(similarity_metric, level_iters=level_iters, step_length=step_length, ss_sigma_factor=ss_sigma_factor, opt_tol=opt_tol, inv_iter=inv_iter, inv_tol=inv_tol)
```

### Step 18: Assign optimizer.verbosity = value

```python
optimizer.verbosity = VerbosityLevels.DEBUG
```

### Step 19: Assign mapping = optimizer.optimize(...)

```python
mapping = optimizer.optimize(static, moving, static_grid2world=None, moving_grid2world=None, prealign=None)
```

### Step 20: Assign m = optimizer.get_map(...)

```python
m = optimizer.get_map()
```

### Step 21: Call assert_equal()

```python
assert_equal(mapping, m)
```

### Step 22: Assign unknown = optimizer.get_intermediate_maps(...)

```python
s2ref, m2ref = optimizer.get_intermediate_maps()
```

### Step 23: Call assert_equal()

```python
assert_equal(s2ref, optimizer.static_to_ref)
```

### Step 24: Call assert_equal()

```python
assert_equal(m2ref, optimizer.moving_to_ref)
```

### Step 25: Assign warped = mapping.transform(...)

```python
warped = mapping.transform(moving)
```

### Step 26: Assign starting_energy = np.sum(...)

```python
starting_energy = np.sum((static - moving) ** 2)
```

### Step 27: Assign final_energy = np.sum(...)

```python
final_energy = np.sum((static - warped) ** 2)
```

### Step 28: Assign reduced = value

```python
reduced = 1.0 - final_energy / starting_energy
```

**Verification:**
```python
assert reduced > 0.9
```


## Complete Example

```python
# Workflow
'Test 3D SyN with CC metric\n\n    Register a volume created by stacking copies of a coronal slice from\n    a T1w brain MRI before and after warping it under a synthetic\n    invertible map. We verify that the final registration is of good\n    quality.\n    '
fname = get_fnames(name='t1_coronal_slice')
nslices = 21
b = 0.1
m = 4
image = np.load(fname)
moving, static = get_warped_stacked_image(image, nslices, b, m)
sigma_diff = 2.0
radius = 2
similarity_metric = metrics.CCMetric(3, sigma_diff=sigma_diff, radius=radius)
level_iters = [20, 5]
step_length = 0.25
opt_tol = 0.0001
inv_iter = 20
inv_tol = 0.001
ss_sigma_factor = 0.2
optimizer = imwarp.SymmetricDiffeomorphicRegistration(similarity_metric, level_iters=level_iters, step_length=step_length, ss_sigma_factor=ss_sigma_factor, opt_tol=opt_tol, inv_iter=inv_iter, inv_tol=inv_tol)
optimizer.verbosity = VerbosityLevels.DEBUG
mapping = optimizer.optimize(static, moving, static_grid2world=None, moving_grid2world=None, prealign=None)
m = optimizer.get_map()
assert_equal(mapping, m)
s2ref, m2ref = optimizer.get_intermediate_maps()
assert_equal(s2ref, optimizer.static_to_ref)
assert_equal(m2ref, optimizer.moving_to_ref)
warped = mapping.transform(moving)
starting_energy = np.sum((static - moving) ** 2)
final_energy = np.sum((static - warped) ** 2)
reduced = 1.0 - final_energy / starting_energy
assert reduced > 0.9
```

## Next Steps


---

*Source: test_imwarp.py:801 | Complexity: Advanced | Last updated: 2026-05-18*