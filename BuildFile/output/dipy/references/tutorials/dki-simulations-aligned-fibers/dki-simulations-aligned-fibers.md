# How To: Dki Simulations Aligned Fibers

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Testing DKI simulations when aligning the same fiber to different axis.

If biological parameters don't change, kt[0] of a fiber aligned to axis x
has to be equal to kt[1] of a fiber aligned to the axis y and equal to
kt[2] of a fiber aligned to axis z. The same is applicable for dt

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.data`
- `dipy.io.gradients`
- `dipy.sims.voxel`
- `dipy.testing.decorators`
- `dipy.reconst.dti`


## Step-by-Step Guide

### Step 1: "\n    Testing DKI simulations when aligning the same fiber to different axis.\n\n    If biological parameters don't change, kt[0] of a fiber aligned to axis x\n    has to be equal to kt[1] of a fiber aligned to the axis y and equal to\n    kt[2] of a fiber aligned to axis z. The same is applicable for dt\n    "

```python
"\n    Testing DKI simulations when aligning the same fiber to different axis.\n\n    If biological parameters don't change, kt[0] of a fiber aligned to axis x\n    has to be equal to kt[1] of a fiber aligned to the axis y and equal to\n    kt[2] of a fiber aligned to axis z. The same is applicable for dt\n    "
```

**Verification:**
```python
assert_array_equal([kt_fx[0], kt_fx[1], kt_fx[2]], [kt_fy[1], kt_fy[0], kt_fy[2]])
```

### Step 2: Assign mevals = np.array(...)

```python
mevals = np.array([[0.00099, 0, 0], [0.00226, 0.00087, 0.00087]])
```

**Verification:**
```python
assert_array_equal([kt_fx[0], kt_fx[1], kt_fx[2]], [kt_fz[2], kt_fz[0], kt_fz[1]])
```

### Step 3: Assign frac = value

```python
frac = [49, 51]
```

**Verification:**
```python
assert_array_equal([dt_fx[0], dt_fx[2], dt_fx[5]], [dt_fy[2], dt_fy[0], dt_fy[5]])
```

### Step 4: Assign angles = value

```python
angles = [(90, 0), (90, 0)]
```

**Verification:**
```python
assert_array_equal([dt_fx[0], dt_fx[2], dt_fx[5]], [dt_fz[5], dt_fz[0], dt_fz[2]])
```

### Step 5: Assign unknown = multi_tensor_dki(...)

```python
signal_fx, dt_fx, kt_fx = multi_tensor_dki(gtab_2s, mevals, angles=angles, fractions=frac)
```

**Verification:**
```python
assert_array_almost_equal(S_fx[0:3], [100, 100, 100])
```

### Step 6: Assign angles = value

```python
angles = [(90, 90), (90, 90)]
```

**Verification:**
```python
assert_array_almost_equal(S_fy[0:3], [100, 100, 100])
```

### Step 7: Assign unknown = multi_tensor_dki(...)

```python
signal_fy, dt_fy, kt_fy = multi_tensor_dki(gtab_2s, mevals, angles=angles, fractions=frac)
```

**Verification:**
```python
assert_array_almost_equal(S_fz[0:3], [100, 100, 100])
```

### Step 8: Assign angles = value

```python
angles = [(0, 0), (0, 0)]
```

**Verification:**
```python
assert_array_almost_equal([S_fx[3], S_fx[4], S_fx[5]], [S_fy[4], S_fy[3], S_fy[5]])
```

### Step 9: Assign unknown = multi_tensor_dki(...)

```python
signal_fz, dt_fz, kt_fz = multi_tensor_dki(gtab_2s, mevals, angles=angles, fractions=frac)
```

**Verification:**
```python
assert_array_almost_equal([S_fx[3], S_fx[4], S_fx[5]], [S_fz[5], S_fz[3], S_fz[4]])
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal([kt_fx[0], kt_fx[1], kt_fx[2]], [kt_fy[1], kt_fy[0], kt_fy[2]])
```

**Verification:**
```python
assert_array_almost_equal([S_fx[6], S_fx[7], S_fx[8]], [S_fy[7], S_fy[6], S_fy[8]])
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal([kt_fx[0], kt_fx[1], kt_fx[2]], [kt_fz[2], kt_fz[0], kt_fz[1]])
```

**Verification:**
```python
assert_array_almost_equal([S_fx[6], S_fx[7], S_fx[8]], [S_fz[8], S_fz[6], S_fz[7]])
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal([dt_fx[0], dt_fx[2], dt_fx[5]], [dt_fy[2], dt_fy[0], dt_fy[5]])
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal([dt_fx[0], dt_fx[2], dt_fx[5]], [dt_fz[5], dt_fz[0], dt_fz[2]])
```

### Step 14: Assign bvals = np.array(...)

```python
bvals = np.array([0, 0, 0, 1000, 1000, 1000, 2000, 2000, 2000])
```

### Step 15: Assign bvecs = np.asarray(...)

```python
bvecs = np.asarray([[1, 0, 0], [0, 1, 0], [0, 0, 1], [1, 0, 0], [0, 1, 0], [0, 0, 1], [1, 0, 0], [0, 1, 0], [0, 0, 1]])
```

### Step 16: Assign gtab_axis = gradient_table(...)

```python
gtab_axis = gradient_table(bvals, bvecs=bvecs)
```

### Step 17: Assign S_fx = dki_signal(...)

```python
S_fx = dki_signal(gtab_axis, dt_fx, kt_fx, S0=100)
```

### Step 18: Call assert_array_almost_equal()

```python
assert_array_almost_equal(S_fx[0:3], [100, 100, 100])
```

### Step 19: Assign S_fy = dki_signal(...)

```python
S_fy = dki_signal(gtab_axis, dt_fy, kt_fy, S0=100)
```

### Step 20: Call assert_array_almost_equal()

```python
assert_array_almost_equal(S_fy[0:3], [100, 100, 100])
```

### Step 21: Assign S_fz = dki_signal(...)

```python
S_fz = dki_signal(gtab_axis, dt_fz, kt_fz, S0=100)
```

### Step 22: Call assert_array_almost_equal()

```python
assert_array_almost_equal(S_fz[0:3], [100, 100, 100])
```

### Step 23: Call assert_array_almost_equal()

```python
assert_array_almost_equal([S_fx[3], S_fx[4], S_fx[5]], [S_fy[4], S_fy[3], S_fy[5]])
```

### Step 24: Call assert_array_almost_equal()

```python
assert_array_almost_equal([S_fx[3], S_fx[4], S_fx[5]], [S_fz[5], S_fz[3], S_fz[4]])
```

### Step 25: Call assert_array_almost_equal()

```python
assert_array_almost_equal([S_fx[6], S_fx[7], S_fx[8]], [S_fy[7], S_fy[6], S_fy[8]])
```

### Step 26: Call assert_array_almost_equal()

```python
assert_array_almost_equal([S_fx[6], S_fx[7], S_fx[8]], [S_fz[8], S_fz[6], S_fz[7]])
```


## Complete Example

```python
# Workflow
"\n    Testing DKI simulations when aligning the same fiber to different axis.\n\n    If biological parameters don't change, kt[0] of a fiber aligned to axis x\n    has to be equal to kt[1] of a fiber aligned to the axis y and equal to\n    kt[2] of a fiber aligned to axis z. The same is applicable for dt\n    "
mevals = np.array([[0.00099, 0, 0], [0.00226, 0.00087, 0.00087]])
frac = [49, 51]
angles = [(90, 0), (90, 0)]
signal_fx, dt_fx, kt_fx = multi_tensor_dki(gtab_2s, mevals, angles=angles, fractions=frac)
angles = [(90, 90), (90, 90)]
signal_fy, dt_fy, kt_fy = multi_tensor_dki(gtab_2s, mevals, angles=angles, fractions=frac)
angles = [(0, 0), (0, 0)]
signal_fz, dt_fz, kt_fz = multi_tensor_dki(gtab_2s, mevals, angles=angles, fractions=frac)
assert_array_equal([kt_fx[0], kt_fx[1], kt_fx[2]], [kt_fy[1], kt_fy[0], kt_fy[2]])
assert_array_equal([kt_fx[0], kt_fx[1], kt_fx[2]], [kt_fz[2], kt_fz[0], kt_fz[1]])
assert_array_equal([dt_fx[0], dt_fx[2], dt_fx[5]], [dt_fy[2], dt_fy[0], dt_fy[5]])
assert_array_equal([dt_fx[0], dt_fx[2], dt_fx[5]], [dt_fz[5], dt_fz[0], dt_fz[2]])
bvals = np.array([0, 0, 0, 1000, 1000, 1000, 2000, 2000, 2000])
bvecs = np.asarray([[1, 0, 0], [0, 1, 0], [0, 0, 1], [1, 0, 0], [0, 1, 0], [0, 0, 1], [1, 0, 0], [0, 1, 0], [0, 0, 1]])
gtab_axis = gradient_table(bvals, bvecs=bvecs)
S_fx = dki_signal(gtab_axis, dt_fx, kt_fx, S0=100)
assert_array_almost_equal(S_fx[0:3], [100, 100, 100])
S_fy = dki_signal(gtab_axis, dt_fy, kt_fy, S0=100)
assert_array_almost_equal(S_fy[0:3], [100, 100, 100])
S_fz = dki_signal(gtab_axis, dt_fz, kt_fz, S0=100)
assert_array_almost_equal(S_fz[0:3], [100, 100, 100])
assert_array_almost_equal([S_fx[3], S_fx[4], S_fx[5]], [S_fy[4], S_fy[3], S_fy[5]])
assert_array_almost_equal([S_fx[3], S_fx[4], S_fx[5]], [S_fz[5], S_fz[3], S_fz[4]])
assert_array_almost_equal([S_fx[6], S_fx[7], S_fx[8]], [S_fy[7], S_fy[6], S_fy[8]])
assert_array_almost_equal([S_fx[6], S_fx[7], S_fx[8]], [S_fz[8], S_fz[6], S_fz[7]])
```

## Next Steps


---

*Source: test_voxel.py:259 | Complexity: Advanced | Last updated: 2026-05-18*