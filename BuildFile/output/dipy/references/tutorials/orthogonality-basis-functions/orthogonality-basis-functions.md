# How To: Orthogonality Basis Functions

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test orthogonality basis functions

## Prerequisites

**Required Modules:**
- `math`
- `platform`
- `time`
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `scipy.integrate`
- `scipy.special`
- `dipy.core.sphere_stats`
- `dipy.core.subdivide_octahedron`
- `dipy.data`
- `dipy.direction.peaks`
- `dipy.reconst`
- `dipy.reconst.mapmri`
- `dipy.reconst.odf`
- `dipy.reconst.shm`
- `dipy.reconst.tests.test_dsi`
- `dipy.sims.voxel`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign diffusivity = 0.0015

```python
diffusivity = 0.0015
```

**Verification:**
```python
assert_almost_equal(int1, 0.0)
```

### Step 2: Assign qmin = 0

```python
qmin = 0
```

**Verification:**
```python
assert_almost_equal(int2, 0.0)
```

### Step 3: Assign qmax = 1000

```python
qmax = 1000
```

**Verification:**
```python
assert_almost_equal(int3, 0.0)
```

### Step 4: Assign int1 = value

```python
int1 = integrate.quad(lambda x: np.real(mapmri.mapmri_phi_1d(0, x, diffusivity)) * np.real(mapmri.mapmri_phi_1d(2, x, diffusivity)), qmin, qmax)[0]
```

**Verification:**
```python
assert_almost_equal(int4, 0.0)
```

### Step 5: Assign int2 = value

```python
int2 = integrate.quad(lambda x: np.real(mapmri.mapmri_phi_1d(2, x, diffusivity)) * np.real(mapmri.mapmri_phi_1d(4, x, diffusivity)), qmin, qmax)[0]
```

**Verification:**
```python
assert_almost_equal(int1, 0.0)
```

### Step 6: Assign int3 = value

```python
int3 = integrate.quad(lambda x: np.real(mapmri.mapmri_phi_1d(4, x, diffusivity)) * np.real(mapmri.mapmri_phi_1d(6, x, diffusivity)), qmin, qmax)[0]
```

**Verification:**
```python
assert_almost_equal(int2, 0.0)
```

### Step 7: Assign int4 = value

```python
int4 = integrate.quad(lambda x: np.real(mapmri.mapmri_phi_1d(6, x, diffusivity)) * np.real(mapmri.mapmri_phi_1d(8, x, diffusivity)), qmin, qmax)[0]
```

**Verification:**
```python
assert_almost_equal(int3, 0.0)
```

### Step 8: Call assert_almost_equal()

```python
assert_almost_equal(int1, 0.0)
```

**Verification:**
```python
assert_almost_equal(int4, 0.0)
```

### Step 9: Call assert_almost_equal()

```python
assert_almost_equal(int2, 0.0)
```

### Step 10: Call assert_almost_equal()

```python
assert_almost_equal(int3, 0.0)
```

### Step 11: Call assert_almost_equal()

```python
assert_almost_equal(int4, 0.0)
```

### Step 12: Call assert_almost_equal()

```python
assert_almost_equal(int1, 0.0)
```

### Step 13: Call assert_almost_equal()

```python
assert_almost_equal(int2, 0.0)
```

### Step 14: Call assert_almost_equal()

```python
assert_almost_equal(int3, 0.0)
```

### Step 15: Call assert_almost_equal()

```python
assert_almost_equal(int4, 0.0)
```

### Step 16: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', category=integrate.IntegrationWarning)
```

### Step 17: Assign int1 = value

```python
int1 = integrate.quad(lambda q: mapmri.mapmri_isotropic_radial_signal_basis(1, 0, diffusivity, q) * mapmri.mapmri_isotropic_radial_signal_basis(2, 0, diffusivity, q) * q ** 2, qmin, qmax)[0]
```

### Step 18: Assign int2 = value

```python
int2 = integrate.quad(lambda q: mapmri.mapmri_isotropic_radial_signal_basis(2, 0, diffusivity, q) * mapmri.mapmri_isotropic_radial_signal_basis(3, 0, diffusivity, q) * q ** 2, qmin, qmax)[0]
```

### Step 19: Assign int3 = value

```python
int3 = integrate.quad(lambda q: mapmri.mapmri_isotropic_radial_signal_basis(3, 0, diffusivity, q) * mapmri.mapmri_isotropic_radial_signal_basis(4, 0, diffusivity, q) * q ** 2, qmin, qmax)[0]
```

### Step 20: Assign int4 = value

```python
int4 = integrate.quad(lambda q: mapmri.mapmri_isotropic_radial_signal_basis(4, 0, diffusivity, q) * mapmri.mapmri_isotropic_radial_signal_basis(5, 0, diffusivity, q) * q ** 2, qmin, qmax)[0]
```


## Complete Example

```python
# Workflow
diffusivity = 0.0015
qmin = 0
qmax = 1000
int1 = integrate.quad(lambda x: np.real(mapmri.mapmri_phi_1d(0, x, diffusivity)) * np.real(mapmri.mapmri_phi_1d(2, x, diffusivity)), qmin, qmax)[0]
int2 = integrate.quad(lambda x: np.real(mapmri.mapmri_phi_1d(2, x, diffusivity)) * np.real(mapmri.mapmri_phi_1d(4, x, diffusivity)), qmin, qmax)[0]
int3 = integrate.quad(lambda x: np.real(mapmri.mapmri_phi_1d(4, x, diffusivity)) * np.real(mapmri.mapmri_phi_1d(6, x, diffusivity)), qmin, qmax)[0]
int4 = integrate.quad(lambda x: np.real(mapmri.mapmri_phi_1d(6, x, diffusivity)) * np.real(mapmri.mapmri_phi_1d(8, x, diffusivity)), qmin, qmax)[0]
assert_almost_equal(int1, 0.0)
assert_almost_equal(int2, 0.0)
assert_almost_equal(int3, 0.0)
assert_almost_equal(int4, 0.0)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', category=integrate.IntegrationWarning)
    int1 = integrate.quad(lambda q: mapmri.mapmri_isotropic_radial_signal_basis(1, 0, diffusivity, q) * mapmri.mapmri_isotropic_radial_signal_basis(2, 0, diffusivity, q) * q ** 2, qmin, qmax)[0]
    int2 = integrate.quad(lambda q: mapmri.mapmri_isotropic_radial_signal_basis(2, 0, diffusivity, q) * mapmri.mapmri_isotropic_radial_signal_basis(3, 0, diffusivity, q) * q ** 2, qmin, qmax)[0]
    int3 = integrate.quad(lambda q: mapmri.mapmri_isotropic_radial_signal_basis(3, 0, diffusivity, q) * mapmri.mapmri_isotropic_radial_signal_basis(4, 0, diffusivity, q) * q ** 2, qmin, qmax)[0]
    int4 = integrate.quad(lambda q: mapmri.mapmri_isotropic_radial_signal_basis(4, 0, diffusivity, q) * mapmri.mapmri_isotropic_radial_signal_basis(5, 0, diffusivity, q) * q ** 2, qmin, qmax)[0]
assert_almost_equal(int1, 0.0)
assert_almost_equal(int2, 0.0)
assert_almost_equal(int3, 0.0)
assert_almost_equal(int4, 0.0)
```

## Next Steps


---

*Source: test_mapmri.py:55 | Complexity: Advanced | Last updated: 2026-05-18*