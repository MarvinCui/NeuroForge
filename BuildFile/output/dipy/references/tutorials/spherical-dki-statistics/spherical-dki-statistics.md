# How To: Spherical Dki Statistics

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test spherical dki statistics

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

### Step 1: Assign MParam = np.zeros(...)

```python
MParam = np.zeros((2, 2, 2, 27))
```

**Verification:**
```python
assert_array_almost_equal(MK_multi, MRef)
```

### Step 2: Assign unknown, unknown, unknown = params_sph

```python
MParam[0, 0, 0] = MParam[0, 0, 1] = MParam[0, 1, 0] = params_sph
```

**Verification:**
```python
assert_array_almost_equal(RK_multi, MRef)
```

### Step 3: Assign unknown, unknown = params_sph

```python
MParam[0, 1, 1] = MParam[1, 1, 0] = params_sph
```

**Verification:**
```python
assert_array_almost_equal(AK_multi, MRef)
```

### Step 4: Assign MRef = np.zeros(...)

```python
MRef = np.zeros((2, 2, 2))
```

**Verification:**
```python
assert_array_almost_equal(MSK_multi, MRef)
```

### Step 5: Assign unknown, unknown, unknown = Kref_sphere

```python
MRef[0, 0, 0] = MRef[0, 0, 1] = MRef[0, 1, 0] = Kref_sphere
```

**Verification:**
```python
assert_array_almost_equal(RKT_multi, MRef)
```

### Step 6: Assign unknown, unknown = Kref_sphere

```python
MRef[0, 1, 1] = MRef[1, 1, 0] = Kref_sphere
```

**Verification:**
```python
assert_array_almost_equal(KFA_multi, 0 * MRef)
```

### Step 7: Assign unknown, unknown, unknown = 0

```python
MRef[1, 1, 1] = MRef[1, 0, 0] = MRef[1, 0, 1] = 0
```

### Step 8: Assign MK_multi = mean_kurtosis(...)

```python
MK_multi = mean_kurtosis(MParam, analytical=True)
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(MK_multi, MRef)
```

### Step 10: Assign RK_multi = radial_kurtosis(...)

```python
RK_multi = radial_kurtosis(MParam, analytical=True)
```

### Step 11: Call assert_array_almost_equal()

```python
assert_array_almost_equal(RK_multi, MRef)
```

### Step 12: Assign AK_multi = axial_kurtosis(...)

```python
AK_multi = axial_kurtosis(MParam, analytical=True)
```

### Step 13: Call assert_array_almost_equal()

```python
assert_array_almost_equal(AK_multi, MRef)
```

### Step 14: Assign MSK_multi = mean_kurtosis_tensor(...)

```python
MSK_multi = mean_kurtosis_tensor(MParam)
```

### Step 15: Call assert_array_almost_equal()

```python
assert_array_almost_equal(MSK_multi, MRef)
```

### Step 16: Assign RKT_multi = radial_tensor_kurtosis(...)

```python
RKT_multi = radial_tensor_kurtosis(MParam)
```

### Step 17: Call assert_array_almost_equal()

```python
assert_array_almost_equal(RKT_multi, MRef)
```

### Step 18: Assign KFA_multi = kurtosis_fractional_anisotropy(...)

```python
KFA_multi = kurtosis_fractional_anisotropy(MParam)
```

### Step 19: Call assert_array_almost_equal()

```python
assert_array_almost_equal(KFA_multi, 0 * MRef)
```


## Complete Example

```python
# Workflow
MParam = np.zeros((2, 2, 2, 27))
MParam[0, 0, 0] = MParam[0, 0, 1] = MParam[0, 1, 0] = params_sph
MParam[0, 1, 1] = MParam[1, 1, 0] = params_sph
MRef = np.zeros((2, 2, 2))
MRef[0, 0, 0] = MRef[0, 0, 1] = MRef[0, 1, 0] = Kref_sphere
MRef[0, 1, 1] = MRef[1, 1, 0] = Kref_sphere
MRef[1, 1, 1] = MRef[1, 0, 0] = MRef[1, 0, 1] = 0
MK_multi = mean_kurtosis(MParam, analytical=True)
assert_array_almost_equal(MK_multi, MRef)
RK_multi = radial_kurtosis(MParam, analytical=True)
assert_array_almost_equal(RK_multi, MRef)
AK_multi = axial_kurtosis(MParam, analytical=True)
assert_array_almost_equal(AK_multi, MRef)
MSK_multi = mean_kurtosis_tensor(MParam)
assert_array_almost_equal(MSK_multi, MRef)
RKT_multi = radial_tensor_kurtosis(MParam)
assert_array_almost_equal(RKT_multi, MRef)
KFA_multi = kurtosis_fractional_anisotropy(MParam)
assert_array_almost_equal(KFA_multi, 0 * MRef)
```

## Next Steps


---

*Source: test_dki.py:714 | Complexity: Advanced | Last updated: 2026-05-18*