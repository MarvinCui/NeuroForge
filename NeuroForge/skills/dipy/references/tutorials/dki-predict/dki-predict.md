# How To: Dki Predict

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test dki predict

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
assert_array_almost_equal(pred, signal_cross)
```

### Step 2: Assign pred = dkiM.predict(...)

```python
pred = dkiM.predict(crossing_ref, S0=100)
```

**Verification:**
```python
assert_array_almost_equal(pred_multi, DWI)
```

### Step 3: Call assert_array_almost_equal()

```python
assert_array_almost_equal(pred, signal_cross)
```

**Verification:**
```python
assert_array_almost_equal(pred_multi, DWI)
```

### Step 4: Assign pred_multi = dkiM.predict(...)

```python
pred_multi = dkiM.predict(multi_params, S0=100)
```

**Verification:**
```python
assert_array_almost_equal(pred_multi, DWI)
```

### Step 5: Call assert_array_almost_equal()

```python
assert_array_almost_equal(pred_multi, DWI)
```

**Verification:**
```python
assert_array_almost_equal(pred_from_fit, DWI)
```

### Step 6: Assign pred_multi = dkiM.predict(...)

```python
pred_multi = dkiM.predict(multi_params, S0=100 * np.ones(pred_multi.shape[:3]))
```

**Verification:**
```python
assert_array_almost_equal(pred, signal_cross)
```

### Step 7: Call assert_array_almost_equal()

```python
assert_array_almost_equal(pred_multi, DWI)
```

**Verification:**
```python
assert_array_almost_equal(pred, DWI)
```

### Step 8: Assign dkiF = dkiM.fit(...)

```python
dkiF = dkiM.fit(DWI)
```

### Step 9: Assign pred_multi = dkiF.predict(...)

```python
pred_multi = dkiF.predict(gtab_2s, S0=100)
```

### Step 10: Call assert_array_almost_equal()

```python
assert_array_almost_equal(pred_multi, DWI)
```

### Step 11: Assign dkiF = dkiM.fit(...)

```python
dkiF = dkiM.fit(pred_multi)
```

### Step 12: Assign pred_from_fit = dkiF.predict(...)

```python
pred_from_fit = dkiF.predict(dkiM.gtab, S0=100)
```

### Step 13: Call assert_array_almost_equal()

```python
assert_array_almost_equal(pred_from_fit, DWI)
```

### Step 14: Assign pred = dki.dki_prediction(...)

```python
pred = dki.dki_prediction(crossing_ref, gtab_2s, S0=100)
```

### Step 15: Call assert_array_almost_equal()

```python
assert_array_almost_equal(pred, signal_cross)
```

### Step 16: Assign pred = dki.dki_prediction(...)

```python
pred = dki.dki_prediction(multi_params, gtab_2s, S0=100 * np.ones(multi_params.shape[:3]))
```

### Step 17: Call assert_array_almost_equal()

```python
assert_array_almost_equal(pred, DWI)
```


## Complete Example

```python
# Workflow
dkiM = dki.DiffusionKurtosisModel(gtab_2s)
pred = dkiM.predict(crossing_ref, S0=100)
assert_array_almost_equal(pred, signal_cross)
pred_multi = dkiM.predict(multi_params, S0=100)
assert_array_almost_equal(pred_multi, DWI)
pred_multi = dkiM.predict(multi_params, S0=100 * np.ones(pred_multi.shape[:3]))
assert_array_almost_equal(pred_multi, DWI)
dkiF = dkiM.fit(DWI)
pred_multi = dkiF.predict(gtab_2s, S0=100)
assert_array_almost_equal(pred_multi, DWI)
dkiF = dkiM.fit(pred_multi)
pred_from_fit = dkiF.predict(dkiM.gtab, S0=100)
assert_array_almost_equal(pred_from_fit, DWI)
pred = dki.dki_prediction(crossing_ref, gtab_2s, S0=100)
assert_array_almost_equal(pred, signal_cross)
pred = dki.dki_prediction(multi_params, gtab_2s, S0=100 * np.ones(multi_params.shape[:3]))
assert_array_almost_equal(pred, DWI)
```

## Next Steps


---

*Source: test_dki.py:446 | Complexity: Advanced | Last updated: 2026-05-18*