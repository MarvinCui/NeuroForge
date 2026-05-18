# How To: Fwdti Predictions

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test fwdti predictions

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.data`
- `dipy.io.gradients`
- `dipy.reconst.dti`
- `dipy.reconst.dti`
- `dipy.reconst.fwdti`
- `dipy.reconst.fwdti`
- `dipy.sims.voxel`


## Step-by-Step Guide

### Step 1: Assign gtf = 0.5

```python
gtf = 0.5
```

**Verification:**
```python
assert_array_almost_equal(S_pred1, S_conta)
```

### Step 2: Assign angles = value

```python
angles = [(90, 0), (90, 0)]
```

**Verification:**
```python
assert_array_almost_equal(S_pred2, S_conta)
```

### Step 3: Assign mevals = np.array(...)

```python
mevals = np.array([[0.0017, 0.0003, 0.0003], [0.003, 0.003, 0.003]])
```

**Verification:**
```python
assert_array_almost_equal(S_pred3, S_conta, decimal=5)
```

### Step 4: Assign unknown = multi_tensor(...)

```python
S_conta, peaks = multi_tensor(gtab_2s, mevals, S0=100, angles=angles, fractions=[(1 - gtf) * 100, gtf * 100], snr=None)
```

**Verification:**
```python
assert_array_almost_equal(S_pred1, DWI)
```

### Step 5: Assign R = all_tensor_evecs(...)

```python
R = all_tensor_evecs(peaks[0])
```

**Verification:**
```python
assert_array_almost_equal(S_pred2, DWI)
```

### Step 6: Assign R = R.reshape(...)

```python
R = R.reshape(9)
```

**Verification:**
```python
assert_array_almost_equal(S_pred3, DWI)
```

### Step 7: Assign model_params = np.concatenate(...)

```python
model_params = np.concatenate(([0.0017, 0.0003, 0.0003], R, [gtf]), axis=0)
```

### Step 8: Assign S_pred1 = fwdti_prediction(...)

```python
S_pred1 = fwdti_prediction(model_params, gtab_2s, S0=100)
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(S_pred1, S_conta)
```

### Step 10: Assign fwdm = fwdti.FreeWaterTensorModel(...)

```python
fwdm = fwdti.FreeWaterTensorModel(gtab_2s)
```

### Step 11: Assign S_pred2 = fwdm.predict(...)

```python
S_pred2 = fwdm.predict(model_params, S0=100)
```

### Step 12: Call assert_array_almost_equal()

```python
assert_array_almost_equal(S_pred2, S_conta)
```

### Step 13: Assign fwefit = fwdm.fit(...)

```python
fwefit = fwdm.fit(S_conta)
```

### Step 14: Assign S_pred3 = fwefit.predict(...)

```python
S_pred3 = fwefit.predict(gtab_2s, S0=100)
```

### Step 15: Call assert_array_almost_equal()

```python
assert_array_almost_equal(S_pred3, S_conta, decimal=5)
```

### Step 16: Assign S_pred1 = fwdti_prediction(...)

```python
S_pred1 = fwdti_prediction(model_params_mv, gtab_2s, S0=100)
```

### Step 17: Call assert_array_almost_equal()

```python
assert_array_almost_equal(S_pred1, DWI)
```

### Step 18: Assign S_pred2 = fwdm.predict(...)

```python
S_pred2 = fwdm.predict(model_params_mv, S0=100)
```

### Step 19: Call assert_array_almost_equal()

```python
assert_array_almost_equal(S_pred2, DWI)
```

### Step 20: Assign fwefit = fwdm.fit(...)

```python
fwefit = fwdm.fit(DWI)
```

### Step 21: Assign S_pred3 = fwefit.predict(...)

```python
S_pred3 = fwefit.predict(gtab_2s, S0=100)
```

### Step 22: Call assert_array_almost_equal()

```python
assert_array_almost_equal(S_pred3, DWI)
```


## Complete Example

```python
# Workflow
gtf = 0.5
angles = [(90, 0), (90, 0)]
mevals = np.array([[0.0017, 0.0003, 0.0003], [0.003, 0.003, 0.003]])
S_conta, peaks = multi_tensor(gtab_2s, mevals, S0=100, angles=angles, fractions=[(1 - gtf) * 100, gtf * 100], snr=None)
R = all_tensor_evecs(peaks[0])
R = R.reshape(9)
model_params = np.concatenate(([0.0017, 0.0003, 0.0003], R, [gtf]), axis=0)
S_pred1 = fwdti_prediction(model_params, gtab_2s, S0=100)
assert_array_almost_equal(S_pred1, S_conta)
fwdm = fwdti.FreeWaterTensorModel(gtab_2s)
S_pred2 = fwdm.predict(model_params, S0=100)
assert_array_almost_equal(S_pred2, S_conta)
fwefit = fwdm.fit(S_conta)
S_pred3 = fwefit.predict(gtab_2s, S0=100)
assert_array_almost_equal(S_pred3, S_conta, decimal=5)
S_pred1 = fwdti_prediction(model_params_mv, gtab_2s, S0=100)
assert_array_almost_equal(S_pred1, DWI)
S_pred2 = fwdm.predict(model_params_mv, S0=100)
assert_array_almost_equal(S_pred2, DWI)
fwefit = fwdm.fit(DWI)
S_pred3 = fwefit.predict(gtab_2s, S0=100)
assert_array_almost_equal(S_pred3, DWI)
```

## Next Steps


---

*Source: test_fwdti.py:178 | Complexity: Advanced | Last updated: 2026-05-18*