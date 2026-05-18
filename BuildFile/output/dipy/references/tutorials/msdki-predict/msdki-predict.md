# How To: Msdki Predict

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test msdki predict

## Prerequisites

**Required Modules:**
- `random`
- `numpy`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.data`
- `dipy.io.gradients`
- `dipy.reconst.msdki`
- `dipy.reconst.msdki`
- `dipy.sims.voxel`


## Step-by-Step Guide

### Step 1: Assign dkiM = msdki.MeanDiffusionKurtosisModel(...)

```python
dkiM = msdki.MeanDiffusionKurtosisModel(gtab_3s)
```

**Verification:**
```python
assert_array_almost_equal(pred, signal_sph)
```

### Step 2: Assign pred = dkiM.predict(...)

```python
pred = dkiM.predict(params_single, S0=100)
```

**Verification:**
```python
assert_array_almost_equal(pred[:, :, 0, :], DWI[:, :, 0, :])
```

### Step 3: Call assert_array_almost_equal()

```python
assert_array_almost_equal(pred, signal_sph)
```

**Verification:**
```python
assert_array_almost_equal(pred_single, signal_sph)
```

### Step 4: Assign pred = dkiM.predict(...)

```python
pred = dkiM.predict(params_multi, S0=100)
```

**Verification:**
```python
assert_array_almost_equal(pred_multi[:, :, 0, :], DWI[:, :, 0, :])
```

### Step 5: Call assert_array_almost_equal()

```python
assert_array_almost_equal(pred[:, :, 0, :], DWI[:, :, 0, :])
```

**Verification:**
```python
assert_array_almost_equal(100 * pred_single, signal_sph)
```

### Step 6: Assign dkiF = dkiM.fit(...)

```python
dkiF = dkiM.fit(signal_sph)
```

**Verification:**
```python
assert_array_almost_equal(100 * pred_multi[:, :, 0, :], DWI[:, :, 0, :])
```

### Step 7: Assign pred_single = dkiF.predict(...)

```python
pred_single = dkiF.predict(gtab_3s, S0=100)
```

**Verification:**
```python
assert_array_almost_equal(pred_multi[:, :, 0, :], DWI[:, :, 0, :])
```

### Step 8: Call assert_array_almost_equal()

```python
assert_array_almost_equal(pred_single, signal_sph)
```

### Step 9: Assign dkiF = dkiM.fit(...)

```python
dkiF = dkiM.fit(DWI)
```

### Step 10: Assign pred_multi = dkiF.predict(...)

```python
pred_multi = dkiF.predict(gtab_3s, S0=100)
```

### Step 11: Call assert_array_almost_equal()

```python
assert_array_almost_equal(pred_multi[:, :, 0, :], DWI[:, :, 0, :])
```

### Step 12: Assign dkiF = dkiM.fit(...)

```python
dkiF = dkiM.fit(signal_sph)
```

### Step 13: Assign pred_single = dkiF.predict(...)

```python
pred_single = dkiF.predict(gtab_3s)
```

### Step 14: Call assert_array_almost_equal()

```python
assert_array_almost_equal(100 * pred_single, signal_sph)
```

### Step 15: Assign dkiF = dkiM.fit(...)

```python
dkiF = dkiM.fit(DWI)
```

### Step 16: Assign pred_multi = dkiF.predict(...)

```python
pred_multi = dkiF.predict(gtab_3s)
```

### Step 17: Call assert_array_almost_equal()

```python
assert_array_almost_equal(100 * pred_multi[:, :, 0, :], DWI[:, :, 0, :])
```

### Step 18: Assign dkiF = dkiM.fit(...)

```python
dkiF = dkiM.fit(DWI)
```

### Step 19: Assign pred_multi = dkiF.predict(...)

```python
pred_multi = dkiF.predict(gtab_3s, S0=100 * np.ones(DWI.shape[:-1]))
```

### Step 20: Call assert_array_almost_equal()

```python
assert_array_almost_equal(pred_multi[:, :, 0, :], DWI[:, :, 0, :])
```


## Complete Example

```python
# Workflow
dkiM = msdki.MeanDiffusionKurtosisModel(gtab_3s)
pred = dkiM.predict(params_single, S0=100)
assert_array_almost_equal(pred, signal_sph)
pred = dkiM.predict(params_multi, S0=100)
assert_array_almost_equal(pred[:, :, 0, :], DWI[:, :, 0, :])
dkiF = dkiM.fit(signal_sph)
pred_single = dkiF.predict(gtab_3s, S0=100)
assert_array_almost_equal(pred_single, signal_sph)
dkiF = dkiM.fit(DWI)
pred_multi = dkiF.predict(gtab_3s, S0=100)
assert_array_almost_equal(pred_multi[:, :, 0, :], DWI[:, :, 0, :])
dkiF = dkiM.fit(signal_sph)
pred_single = dkiF.predict(gtab_3s)
assert_array_almost_equal(100 * pred_single, signal_sph)
dkiF = dkiM.fit(DWI)
pred_multi = dkiF.predict(gtab_3s)
assert_array_almost_equal(100 * pred_multi[:, :, 0, :], DWI[:, :, 0, :])
dkiF = dkiM.fit(DWI)
pred_multi = dkiF.predict(gtab_3s, S0=100 * np.ones(DWI.shape[:-1]))
assert_array_almost_equal(pred_multi[:, :, 0, :], DWI[:, :, 0, :])
```

## Next Steps


---

*Source: test_msdki.py:103 | Complexity: Advanced | Last updated: 2026-05-18*