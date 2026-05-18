# How To: Dki Micro Predict Multi Voxel

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test dki micro predict multi voxel

## Prerequisites

**Required Modules:**
- `random`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.core.gradients`
- `dipy.data`
- `dipy.io.gradients`
- `dipy.reconst.dki`
- `dipy.reconst.dki_micro`
- `dipy.reconst.dti`
- `dipy.sims.voxel`
- `dipy.utils.optpkg`


## Step-by-Step Guide

### Step 1: Assign dkiM = dki_micro.KurtosisMicrostructureModel(...)

```python
dkiM = dki_micro.KurtosisMicrostructureModel(gtab_2s)
```

**Verification:**
```python
assert_array_almost_equal(pred, DWIsim_all_taylor, decimal=3)
```

### Step 2: Assign dkiF = dkiM.fit(...)

```python
dkiF = dkiM.fit(DWIsim)
```

**Verification:**
```python
assert_array_almost_equal(pred, DWIsim_all_taylor * 100, decimal=3)
```

### Step 3: Assign pred = dkiM.predict(...)

```python
pred = dkiM.predict(dkiF.model_params)
```

**Verification:**
```python
assert_array_almost_equal(pred, DWIsim_all_taylor * 100, decimal=3)
```

### Step 4: Call assert_array_almost_equal()

```python
assert_array_almost_equal(pred, DWIsim_all_taylor, decimal=3)
```

### Step 5: Assign pred = dkiM.predict(...)

```python
pred = dkiM.predict(dkiF.model_params, S0=100)
```

### Step 6: Call assert_array_almost_equal()

```python
assert_array_almost_equal(pred, DWIsim_all_taylor * 100, decimal=3)
```

### Step 7: Assign pred = dkiF.predict(...)

```python
pred = dkiF.predict(gtab_2s, S0=100)
```

### Step 8: Call assert_array_almost_equal()

```python
assert_array_almost_equal(pred, DWIsim_all_taylor * 100, decimal=3)
```


## Complete Example

```python
# Workflow
dkiM = dki_micro.KurtosisMicrostructureModel(gtab_2s)
dkiF = dkiM.fit(DWIsim)
pred = dkiM.predict(dkiF.model_params)
assert_array_almost_equal(pred, DWIsim_all_taylor, decimal=3)
pred = dkiM.predict(dkiF.model_params, S0=100)
assert_array_almost_equal(pred, DWIsim_all_taylor * 100, decimal=3)
pred = dkiF.predict(gtab_2s, S0=100)
assert_array_almost_equal(pred, DWIsim_all_taylor * 100, decimal=3)
```

## Next Steps


---

*Source: test_dki_micro.py:330 | Complexity: Advanced | Last updated: 2026-05-18*