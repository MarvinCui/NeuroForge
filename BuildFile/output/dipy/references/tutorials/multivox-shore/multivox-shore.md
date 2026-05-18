# How To: Multivox Shore

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test multivox shore

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `dipy.core.sphere_stats`
- `dipy.core.subdivide_octahedron`
- `dipy.data`
- `dipy.direction.peaks`
- `dipy.reconst.odf`
- `dipy.reconst.shm`
- `dipy.reconst.shore`
- `dipy.reconst.tests.test_dsi`
- `dipy.sims.voxel`
- `dipy.testing.decorators`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign gtab = get_3shell_gtab(...)

```python
gtab = get_3shell_gtab()
```

### Step 2: Assign data = rng.random(...)

```python
data = rng.random([20, 30, 1, gtab.gradients.shape[0]])
```

### Step 3: Assign radial_order = 4

```python
radial_order = 4
```

### Step 4: Assign zeta = 700

```python
zeta = 700
```

### Step 5: Assign asm = ShoreModel(...)

```python
asm = ShoreModel(gtab, radial_order=radial_order, zeta=zeta, lambdaN=1e-08, lambdaL=1e-08)
```

### Step 6: Assign c_shore = value

```python
c_shore = asmfit.shore_coeff
```

### Step 7: Call npt.assert_equal()

```python
npt.assert_equal(c_shore.shape[0:3], data.shape[0:3])
```

### Step 8: Call npt.assert_equal()

```python
npt.assert_equal(np.all(np.isreal(c_shore)), True)
```

### Step 9: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
```

### Step 10: Assign asmfit = asm.fit(...)

```python
asmfit = asm.fit(data)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
gtab = get_3shell_gtab()
data = rng.random([20, 30, 1, gtab.gradients.shape[0]])
radial_order = 4
zeta = 700
asm = ShoreModel(gtab, radial_order=radial_order, zeta=zeta, lambdaN=1e-08, lambdaL=1e-08)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=descoteaux07_legacy_msg, category=PendingDeprecationWarning)
    asmfit = asm.fit(data)
c_shore = asmfit.shore_coeff
npt.assert_equal(c_shore.shape[0:3], data.shape[0:3])
npt.assert_equal(np.all(np.isreal(c_shore)), True)
```

## Next Steps


---

*Source: test_shore_odf.py:97 | Complexity: Advanced | Last updated: 2026-05-18*