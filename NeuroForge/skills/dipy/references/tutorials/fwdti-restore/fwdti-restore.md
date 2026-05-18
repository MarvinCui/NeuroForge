# How To: Fwdti Restore

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test fwdti restore

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
assert_array_almost_equal(fwdtiF.fa, FAdti)
```

### Step 2: Assign mevals = np.array(...)

```python
mevals = np.array([[0.0017, 0.0003, 0.0003], [0.003, 0.003, 0.003]])
```

**Verification:**
```python
assert_array_almost_equal(fwdtiF.f, gtf)
```

### Step 3: Assign unknown = multi_tensor(...)

```python
S_conta, peaks = multi_tensor(gtab_2s, mevals, S0=100, angles=[(90, 0), (90, 0)], fractions=[(1 - gtf) * 100, gtf * 100], snr=None)
```

**Verification:**
```python
assert_array_almost_equal(fwdtiF2.fa, FAdti)
```

### Step 4: Assign fwdm = fwdti.FreeWaterTensorModel(...)

```python
fwdm = fwdti.FreeWaterTensorModel(gtab_2s, fit_method='NLS', weighting='sigma', sigma=4)
```

**Verification:**
```python
assert_array_almost_equal(fwdtiF2.f, gtf)
```

### Step 5: Assign fwdtiF = fwdm.fit(...)

```python
fwdtiF = fwdm.fit(S_conta)
```

### Step 6: Call assert_array_almost_equal()

```python
assert_array_almost_equal(fwdtiF.fa, FAdti)
```

### Step 7: Call assert_array_almost_equal()

```python
assert_array_almost_equal(fwdtiF.f, gtf)
```

### Step 8: Assign fwdm2 = fwdti.FreeWaterTensorModel(...)

```python
fwdm2 = fwdti.FreeWaterTensorModel(gtab_2s, fit_method='NLS', weighting='gmm')
```

### Step 9: Assign fwdtiF2 = fwdm2.fit(...)

```python
fwdtiF2 = fwdm2.fit(S_conta)
```

### Step 10: Call assert_array_almost_equal()

```python
assert_array_almost_equal(fwdtiF2.fa, FAdti)
```

### Step 11: Call assert_array_almost_equal()

```python
assert_array_almost_equal(fwdtiF2.f, gtf)
```


## Complete Example

```python
# Workflow
gtf = 0.5
mevals = np.array([[0.0017, 0.0003, 0.0003], [0.003, 0.003, 0.003]])
S_conta, peaks = multi_tensor(gtab_2s, mevals, S0=100, angles=[(90, 0), (90, 0)], fractions=[(1 - gtf) * 100, gtf * 100], snr=None)
fwdm = fwdti.FreeWaterTensorModel(gtab_2s, fit_method='NLS', weighting='sigma', sigma=4)
fwdtiF = fwdm.fit(S_conta)
assert_array_almost_equal(fwdtiF.fa, FAdti)
assert_array_almost_equal(fwdtiF.f, gtf)
fwdm2 = fwdti.FreeWaterTensorModel(gtab_2s, fit_method='NLS', weighting='gmm')
fwdtiF2 = fwdm2.fit(S_conta)
assert_array_almost_equal(fwdtiF2.fa, FAdti)
assert_array_almost_equal(fwdtiF2.f, gtf)
```

## Next Steps


---

*Source: test_fwdti.py:242 | Complexity: Advanced | Last updated: 2026-05-18*