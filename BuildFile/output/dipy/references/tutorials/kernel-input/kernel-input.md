# How To: Kernel Input

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test the kernel for inputs of type Sphere, type int and for input None

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `dipy.core.sphere`
- `dipy.denoise.enhancement_kernel`
- `dipy.denoise.shift_twist_convolution`
- `dipy.reconst.shm`


## Step-by-Step Guide

### Step 1: 'Test the kernel for inputs of type Sphere, type int and for input None'

```python
'Test the kernel for inputs of type Sphere, type int and for input None'
```

### Step 2: Assign sph = Sphere(...)

```python
sph = Sphere(x=1, y=0, z=0)
```

### Step 3: Assign D33 = 1.0

```python
D33 = 1.0
```

### Step 4: Assign D44 = 0.04

```python
D44 = 0.04
```

### Step 5: Assign t = 1

```python
t = 1
```

### Step 6: Assign k = EnhancementKernel(...)

```python
k = EnhancementKernel(D33, D44, t, orientations=sph, force_recompute=True)
```

### Step 7: Call npt.assert_equal()

```python
npt.assert_equal(k.get_lookup_table().shape, (1, 1, 7, 7, 7))
```

### Step 8: Assign num_orientations = 2

```python
num_orientations = 2
```

### Step 9: Assign k = EnhancementKernel(...)

```python
k = EnhancementKernel(D33, D44, t, orientations=num_orientations, force_recompute=True)
```

### Step 10: Call npt.assert_equal()

```python
npt.assert_equal(k.get_lookup_table().shape, (2, 2, 7, 7, 7))
```

### Step 11: Assign k = EnhancementKernel(...)

```python
k = EnhancementKernel(D33, D44, t, orientations=0, force_recompute=True)
```

### Step 12: Call npt.assert_equal()

```python
npt.assert_equal(k.get_lookup_table().shape, (0, 0, 7, 7, 7))
```


## Complete Example

```python
# Workflow
'Test the kernel for inputs of type Sphere, type int and for input None'
sph = Sphere(x=1, y=0, z=0)
D33 = 1.0
D44 = 0.04
t = 1
k = EnhancementKernel(D33, D44, t, orientations=sph, force_recompute=True)
npt.assert_equal(k.get_lookup_table().shape, (1, 1, 7, 7, 7))
num_orientations = 2
k = EnhancementKernel(D33, D44, t, orientations=num_orientations, force_recompute=True)
npt.assert_equal(k.get_lookup_table().shape, (2, 2, 7, 7, 7))
k = EnhancementKernel(D33, D44, t, orientations=0, force_recompute=True)
npt.assert_equal(k.get_lookup_table().shape, (0, 0, 7, 7, 7))
```

## Next Steps


---

*Source: test_kernel.py:153 | Complexity: Advanced | Last updated: 2026-05-18*