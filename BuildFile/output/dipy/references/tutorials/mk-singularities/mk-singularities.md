# How To: Mk Singularities

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test MK singularities

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

### Step 1: Assign dkiM = dki.DiffusionKurtosisModel(...)

```python
dkiM = dki.DiffusionKurtosisModel(gtab_2s)
```

**Verification:**
```python
assert_almost_equal(MK_an, MK_nm, decimal=3)
```

### Step 2: Assign angles_all = np.array(...)

```python
angles_all = np.array([[(90, 0), (90, 0), (0, 0), (0, 0)], [(89.9, 0), (89.9, 0), (0, 0), (0, 0)]])
```

**Verification:**
```python
assert_almost_equal(MK_an, MK_nm, decimal=3)
```

### Step 3: Assign unknown = multi_tensor_dki(...)

```python
s_90, dt_90, kt_90 = multi_tensor_dki(gtab_2s, mevals_cross, S0=100, angles=angles_90, fractions=frac_cross, snr=None)
```

### Step 4: Assign dkiF = dkiM.fit(...)

```python
dkiF = dkiM.fit(s_90)
```

### Step 5: Assign MK_an = dkiF.mk(...)

```python
MK_an = dkiF.mk(analytical=True)
```

### Step 6: Assign MK_nm = dkiF.mk(...)

```python
MK_nm = dkiF.mk(analytical=False)
```

### Step 7: Call assert_almost_equal()

```python
assert_almost_equal(MK_an, MK_nm, decimal=3)
```

### Step 8: Assign dki_params = dkiF.model_params.copy(...)

```python
dki_params = dkiF.model_params.copy()
```

### Step 9: Assign unknown = value

```python
dki_params[1] = dkiF.model_params[2]
```

### Step 10: Assign unknown = value

```python
dki_params[2] = dkiF.model_params[1]
```

### Step 11: Assign unknown = value

```python
dki_params[4] = dkiF.model_params[5]
```

### Step 12: Assign unknown = value

```python
dki_params[5] = dkiF.model_params[4]
```

### Step 13: Assign unknown = value

```python
dki_params[7] = dkiF.model_params[8]
```

### Step 14: Assign unknown = value

```python
dki_params[8] = dkiF.model_params[7]
```

### Step 15: Assign unknown = value

```python
dki_params[10] = dkiF.model_params[11]
```

### Step 16: Assign unknown = value

```python
dki_params[11] = dkiF.model_params[10]
```

### Step 17: Assign MK_an = dki.mean_kurtosis(...)

```python
MK_an = dki.mean_kurtosis(dki_params, analytical=True)
```

### Step 18: Assign MK_nm = dki.mean_kurtosis(...)

```python
MK_nm = dki.mean_kurtosis(dki_params, analytical=False)
```

### Step 19: Call assert_almost_equal()

```python
assert_almost_equal(MK_an, MK_nm, decimal=3)
```


## Complete Example

```python
# Workflow
dkiM = dki.DiffusionKurtosisModel(gtab_2s)
angles_all = np.array([[(90, 0), (90, 0), (0, 0), (0, 0)], [(89.9, 0), (89.9, 0), (0, 0), (0, 0)]])
for angles_90 in angles_all:
    s_90, dt_90, kt_90 = multi_tensor_dki(gtab_2s, mevals_cross, S0=100, angles=angles_90, fractions=frac_cross, snr=None)
    dkiF = dkiM.fit(s_90)
    MK_an = dkiF.mk(analytical=True)
    MK_nm = dkiF.mk(analytical=False)
    assert_almost_equal(MK_an, MK_nm, decimal=3)
    dki_params = dkiF.model_params.copy()
    dki_params[1] = dkiF.model_params[2]
    dki_params[2] = dkiF.model_params[1]
    dki_params[4] = dkiF.model_params[5]
    dki_params[5] = dkiF.model_params[4]
    dki_params[7] = dkiF.model_params[8]
    dki_params[8] = dkiF.model_params[7]
    dki_params[10] = dkiF.model_params[11]
    dki_params[11] = dkiF.model_params[10]
    MK_an = dki.mean_kurtosis(dki_params, analytical=True)
    MK_nm = dki.mean_kurtosis(dki_params, analytical=False)
    assert_almost_equal(MK_an, MK_nm, decimal=3)
```

## Next Steps


---

*Source: test_dki.py:837 | Complexity: Advanced | Last updated: 2026-05-18*