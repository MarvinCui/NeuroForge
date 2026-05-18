# How To: Cc 2D

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test 2D SyN with CC metric

Register a coronal slice from a T1w brain MRI before and after warping
it under a synthetic invertible map. We verify that the final
registration is of good quality.

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

### Step 1: 'Test 2D SyN with CC metric\n\n    Register a coronal slice from a T1w brain MRI before and after warping\n    it under a synthetic invertible map. We verify that the final\n    registration is of good quality.\n    '

```python
'Test 2D SyN with CC metric\n\n    Register a coronal slice from a T1w brain MRI before and after warping\n    it under a synthetic invertible map. We verify that the final\n    registration is of good quality.\n    '
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

### Step 3: Assign nslices = 1

```python
nslices = 1
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

### Step 8: Assign sigma_diff = 3.0

```python
sigma_diff = 3.0
```

### Step 9: Assign radius = 4

```python
radius = 4
```

### Step 10: Assign metric = metrics.CCMetric(...)

```python
metric = metrics.CCMetric(2, sigma_diff=sigma_diff, radius=radius)
```

### Step 11: Assign level_iters = value

```python
level_iters = [15, 5]
```

### Step 12: Assign optimizer = imwarp.SymmetricDiffeomorphicRegistration(...)

```python
optimizer = imwarp.SymmetricDiffeomorphicRegistration(metric=metric, level_iters=level_iters)
```

### Step 13: Assign optimizer.verbosity = value

```python
optimizer.verbosity = VerbosityLevels.DEBUG
```

### Step 14: Assign mapping = optimizer.optimize(...)

```python
mapping = optimizer.optimize(static, moving, static_grid2world=None)
```

### Step 15: Assign m = optimizer.get_map(...)

```python
m = optimizer.get_map()
```

### Step 16: Call assert_equal()

```python
assert_equal(mapping, m)
```

### Step 17: Assign unknown = optimizer.get_intermediate_maps(...)

```python
s2ref, m2ref = optimizer.get_intermediate_maps()
```

### Step 18: Call assert_equal()

```python
assert_equal(s2ref, optimizer.static_to_ref)
```

### Step 19: Call assert_equal()

```python
assert_equal(m2ref, optimizer.moving_to_ref)
```

### Step 20: Assign warped = mapping.transform(...)

```python
warped = mapping.transform(moving)
```

### Step 21: Assign starting_energy = np.sum(...)

```python
starting_energy = np.sum((static - moving) ** 2)
```

### Step 22: Assign final_energy = np.sum(...)

```python
final_energy = np.sum((static - warped) ** 2)
```

### Step 23: Assign reduced = value

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
'Test 2D SyN with CC metric\n\n    Register a coronal slice from a T1w brain MRI before and after warping\n    it under a synthetic invertible map. We verify that the final\n    registration is of good quality.\n    '
fname = get_fnames(name='t1_coronal_slice')
nslices = 1
b = 0.1
m = 4
image = np.load(fname)
moving, static = get_warped_stacked_image(image, nslices, b, m)
sigma_diff = 3.0
radius = 4
metric = metrics.CCMetric(2, sigma_diff=sigma_diff, radius=radius)
level_iters = [15, 5]
optimizer = imwarp.SymmetricDiffeomorphicRegistration(metric=metric, level_iters=level_iters)
optimizer.verbosity = VerbosityLevels.DEBUG
mapping = optimizer.optimize(static, moving, static_grid2world=None)
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

*Source: test_imwarp.py:760 | Complexity: Advanced | Last updated: 2026-05-18*