# How To: Wrotate Crossing Fibers

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test Wrotate crossing fibers

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

### Step 1: Assign angles = value

```python
angles = [(90, 30), (90, 30), (20, 30), (20, 30)]
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
frac = [fie * 50, (1 - fie) * 50, fie * 50, (1 - fie) * 50]
```

### Step 4: Assign mevals = np.array(...)

```python
mevals = np.array([[0.00099, 0, 0], [0.00226, 0.00087, 0.00087], [0.00099, 0, 0], [0.00226, 0.00087, 0.00087]])
```

### Step 5: Assign unknown = multi_tensor_dki(...)

```python
signal, dt, kt = multi_tensor_dki(gtab_2s, mevals, angles=angles, fractions=frac, snr=None)
```

### Step 6: Assign unknown = decompose_tensor(...)

```python
evals, evecs = decompose_tensor(from_lower_triangular(dt))
```

### Step 7: Assign kt_rotated = dki.Wrotate(...)

```python
kt_rotated = dki.Wrotate(kt, evecs)
```

### Step 8: Assign angles = value

```python
angles = [(90, 35), (90, 35), (90, -35), (90, -35)]
```

### Step 9: Assign unknown = multi_tensor_dki(...)

```python
signal, dt, kt_ref = multi_tensor_dki(gtab_2s, mevals, angles=angles, fractions=frac, snr=None)
```

### Step 10: Call assert_array_almost_equal()

```python
assert_array_almost_equal(kt_rotated, kt_ref)
```


## Complete Example

```python
# Workflow
angles = [(90, 30), (90, 30), (20, 30), (20, 30)]
fie = 0.49
frac = [fie * 50, (1 - fie) * 50, fie * 50, (1 - fie) * 50]
mevals = np.array([[0.00099, 0, 0], [0.00226, 0.00087, 0.00087], [0.00099, 0, 0], [0.00226, 0.00087, 0.00087]])
signal, dt, kt = multi_tensor_dki(gtab_2s, mevals, angles=angles, fractions=frac, snr=None)
evals, evecs = decompose_tensor(from_lower_triangular(dt))
kt_rotated = dki.Wrotate(kt, evecs)
angles = [(90, 35), (90, 35), (90, -35), (90, -35)]
signal, dt, kt_ref = multi_tensor_dki(gtab_2s, mevals, angles=angles, fractions=frac, snr=None)
assert_array_almost_equal(kt_rotated, kt_ref)
```

## Next Steps


---

*Source: test_dki.py:594 | Complexity: Advanced | Last updated: 2026-05-18*