# How To: Dki Micro Predict Single Voxel

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test dki micro predict single voxel

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

### Step 1: Assign fie = 0.49

```python
fie = 0.49
```

**Verification:**
```python
assert_array_almost_equal(pred, signal_gt, decimal=4)
```

### Step 2: Assign ADi = 0.00099

```python
ADi = 0.00099
```

**Verification:**
```python
assert_array_almost_equal(pred, signal_gt * 100, decimal=4)
```

### Step 3: Assign ADe = 0.00226

```python
ADe = 0.00226
```

**Verification:**
```python
assert_array_almost_equal(pred, signal_gt * 100, decimal=4)
```

### Step 4: Assign RDi = 0

```python
RDi = 0
```

### Step 5: Assign RDe = 0.00087

```python
RDe = 0.00087
```

### Step 6: Assign theta = random.uniform(...)

```python
theta = random.uniform(0, 180)
```

### Step 7: Assign phi = random.uniform(...)

```python
phi = random.uniform(0, 320)
```

### Step 8: Assign angles = value

```python
angles = [(theta, phi), (theta, phi)]
```

### Step 9: Assign mevals = np.array(...)

```python
mevals = np.array([[ADi, RDi, RDi], [ADe, RDe, RDe]])
```

### Step 10: Assign frac = value

```python
frac = [fie * 100, (1 - fie) * 100]
```

### Step 11: Assign unknown = multi_tensor_dki(...)

```python
signal, dt, kt = multi_tensor_dki(gtab_2s, mevals, angles=angles, fractions=frac, snr=None)
```

### Step 12: Assign unknown = multi_tensor(...)

```python
signal_gt, da = multi_tensor(gtab_2s, mevals, angles=angles, fractions=frac, snr=None)
```

### Step 13: Assign dkiM = dki_micro.KurtosisMicrostructureModel(...)

```python
dkiM = dki_micro.KurtosisMicrostructureModel(gtab_2s)
```

### Step 14: Assign dkiF = dkiM.fit(...)

```python
dkiF = dkiM.fit(signal)
```

### Step 15: Assign pred = dkiM.predict(...)

```python
pred = dkiM.predict(dkiF.model_params)
```

### Step 16: Call assert_array_almost_equal()

```python
assert_array_almost_equal(pred, signal_gt, decimal=4)
```

### Step 17: Assign pred = dkiM.predict(...)

```python
pred = dkiM.predict(dkiF.model_params, S0=100)
```

### Step 18: Call assert_array_almost_equal()

```python
assert_array_almost_equal(pred, signal_gt * 100, decimal=4)
```

### Step 19: Assign pred = dkiF.predict(...)

```python
pred = dkiF.predict(gtab_2s, S0=100)
```

### Step 20: Call assert_array_almost_equal()

```python
assert_array_almost_equal(pred, signal_gt * 100, decimal=4)
```


## Complete Example

```python
# Workflow
fie = 0.49
ADi = 0.00099
ADe = 0.00226
RDi = 0
RDe = 0.00087
theta = random.uniform(0, 180)
phi = random.uniform(0, 320)
angles = [(theta, phi), (theta, phi)]
mevals = np.array([[ADi, RDi, RDi], [ADe, RDe, RDe]])
frac = [fie * 100, (1 - fie) * 100]
signal, dt, kt = multi_tensor_dki(gtab_2s, mevals, angles=angles, fractions=frac, snr=None)
signal_gt, da = multi_tensor(gtab_2s, mevals, angles=angles, fractions=frac, snr=None)
dkiM = dki_micro.KurtosisMicrostructureModel(gtab_2s)
dkiF = dkiM.fit(signal)
pred = dkiM.predict(dkiF.model_params)
assert_array_almost_equal(pred, signal_gt, decimal=4)
pred = dkiM.predict(dkiF.model_params, S0=100)
assert_array_almost_equal(pred, signal_gt * 100, decimal=4)
pred = dkiF.predict(gtab_2s, S0=100)
assert_array_almost_equal(pred, signal_gt * 100, decimal=4)
```

## Next Steps


---

*Source: test_dki_micro.py:291 | Complexity: Advanced | Last updated: 2026-05-18*