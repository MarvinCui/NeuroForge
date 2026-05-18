# How To: Wrotate Single Fiber

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test Wrotate single fiber

## Prerequisites

**Required Modules:**
- `random`
- `warnings`
- `numpy`
- `numpy.testing`
- `dipy.core.geometry`
- `dipy.core.gradients`
- `dipy.core.sphere`
- `dipy.data`
- `dipy.io.gradients`
- `dipy.reconst.dki`
- `dipy.reconst.dki`
- `dipy.reconst.dti`
- `dipy.reconst.dti`
- `dipy.reconst.utils`
- `dipy.reconst.weights_method`
- `dipy.sims.voxel`
- `dipy.testing`
- `dipy.utils.optpkg`
- `dipy.utils.tripwire`


## Step-by-Step Guide

### Step 1: Assign mevals = np.array(...)

```python
mevals = np.array([[0.00099, 0, 0], [0.00226, 0.00087, 0.00087]])
```

**Verification:**
```python
assert_array_almost_equal(kt_rotated, kt_ref)
```

### Step 2: Assign fie = 0.49

```python
fie = 0.49
```

### Step 3: Assign frac = value

```python
frac = [fie * 100, (1 - fie) * 100]
```

### Step 4: Assign theta = random.uniform(...)

```python
theta = random.uniform(0, 180)
```

### Step 5: Assign phi = random.uniform(...)

```python
phi = random.uniform(0, 320)
```

### Step 6: Assign angles = value

```python
angles = [(theta, phi), (theta, phi)]
```

### Step 7: Assign unknown = multi_tensor_dki(...)

```python
signal, dt, kt = multi_tensor_dki(gtab_2s, mevals, angles=angles, fractions=frac, snr=None)
```

### Step 8: Assign unknown = decompose_tensor(...)

```python
evals, evecs = decompose_tensor(from_lower_triangular(dt))
```

### Step 9: Assign kt_rotated = dki.Wrotate(...)

```python
kt_rotated = dki.Wrotate(kt, evecs)
```

### Step 10: Assign angles = value

```python
angles = ((90, 0), (90, 0))
```

### Step 11: Assign unknown = multi_tensor_dki(...)

```python
signal, dt_ref, kt_ref = multi_tensor_dki(gtab_2s, mevals, angles=angles, fractions=frac, snr=None)
```

### Step 12: Call assert_array_almost_equal()

```python
assert_array_almost_equal(kt_rotated, kt_ref)
```


## Complete Example

```python
# Workflow
mevals = np.array([[0.00099, 0, 0], [0.00226, 0.00087, 0.00087]])
fie = 0.49
frac = [fie * 100, (1 - fie) * 100]
theta = random.uniform(0, 180)
phi = random.uniform(0, 320)
angles = [(theta, phi), (theta, phi)]
signal, dt, kt = multi_tensor_dki(gtab_2s, mevals, angles=angles, fractions=frac, snr=None)
evals, evecs = decompose_tensor(from_lower_triangular(dt))
kt_rotated = dki.Wrotate(kt, evecs)
angles = ((90, 0), (90, 0))
signal, dt_ref, kt_ref = multi_tensor_dki(gtab_2s, mevals, angles=angles, fractions=frac, snr=None)
assert_array_almost_equal(kt_rotated, kt_ref)
```

## Next Steps


---

*Source: test_dki.py:561 | Complexity: Advanced | Last updated: 2026-05-18*