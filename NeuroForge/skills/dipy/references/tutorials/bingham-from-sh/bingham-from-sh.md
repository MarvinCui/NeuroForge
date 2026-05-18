# How To: Bingham From Sh

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test bingham from sh

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.data`
- `dipy.io.gradients`
- `dipy.io.image`
- `dipy.reconst.bingham`
- `dipy.reconst.shm`


## Step-by-Step Guide

### Step 1: Assign ma_axis = np.array(...)

```python
ma_axis = np.array([0, 1, 0])
```

**Verification:**
```python
assert_array_almost_equal(bim_sh.model_params, bim_odf.model_params, decimal=3)
```

### Step 2: Assign mi_axis = np.array(...)

```python
mi_axis = np.array([0, 0, 1])
```

### Step 3: Assign k1 = 2

```python
k1 = 2
```

### Step 4: Assign k2 = 6

```python
k2 = 6
```

### Step 5: Assign f0 = 3

```python
f0 = 3
```

### Step 6: Assign odf = _single_bingham_to_sf(...)

```python
odf = _single_bingham_to_sf(f0, k1, k2, ma_axis, mi_axis, sphere.vertices)
```

### Step 7: Assign bim_odf = sf_to_bingham(...)

```python
bim_odf = sf_to_bingham(odf, sphere, npeaks=2, max_search_angle=45)
```

### Step 8: Assign sh = sf_to_sh(...)

```python
sh = sf_to_sh(odf, sphere, sh_order_max=16, legacy=False)
```

### Step 9: Assign bim_sh = sh_to_bingham(...)

```python
bim_sh = sh_to_bingham(sh, sphere, legacy=False, npeaks=2, max_search_angle=45)
```

### Step 10: Call assert_array_almost_equal()

```python
assert_array_almost_equal(bim_sh.model_params, bim_odf.model_params, decimal=3)
```


## Complete Example

```python
# Workflow
ma_axis = np.array([0, 1, 0])
mi_axis = np.array([0, 0, 1])
k1 = 2
k2 = 6
f0 = 3
odf = _single_bingham_to_sf(f0, k1, k2, ma_axis, mi_axis, sphere.vertices)
bim_odf = sf_to_bingham(odf, sphere, npeaks=2, max_search_angle=45)
sh = sf_to_sh(odf, sphere, sh_order_max=16, legacy=False)
bim_sh = sh_to_bingham(sh, sphere, legacy=False, npeaks=2, max_search_angle=45)
assert_array_almost_equal(bim_sh.model_params, bim_odf.model_params, decimal=3)
```

## Next Steps


---

*Source: test_bingham.py:217 | Complexity: Advanced | Last updated: 2026-05-18*