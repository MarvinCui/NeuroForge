# How To: Fwdti Singlevoxel

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test fwdti singlevoxel

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

### Step 1: Assign gtf = 0.44444

```python
gtf = 0.44444
```

**Verification:**
```python
assert_almost_equal(FAdti, FAfwe, decimal=3)
```

### Step 2: Assign mevals = np.array(...)

```python
mevals = np.array([[0.0017, 0.0003, 0.0003], [0.003, 0.003, 0.003]])
```

**Verification:**
```python
assert_almost_equal(Ffwe, gtf, decimal=3)
```

### Step 3: Assign unknown = multi_tensor(...)

```python
S_conta, peaks = multi_tensor(gtab_2s, mevals, S0=100, angles=[(90, 0), (90, 0)], fractions=[(1 - gtf) * 100, gtf * 100], snr=None)
```

**Verification:**
```python
assert_almost_equal(MDfwe, MDdti, decimal=3)
```

### Step 4: Assign fwdm = fwdti.FreeWaterTensorModel(...)

```python
fwdm = fwdti.FreeWaterTensorModel(gtab_2s, fit_method='WLS')
```

**Verification:**
```python
assert_almost_equal(FAdti, FAfwe)
```

### Step 5: Assign fwefit = fwdm.fit(...)

```python
fwefit = fwdm.fit(S_conta)
```

**Verification:**
```python
assert_almost_equal(Ffwe, gtf)
```

### Step 6: Assign FAfwe = value

```python
FAfwe = fwefit.fa
```

**Verification:**
```python
assert_almost_equal(MDfwe, MDdti)
```

### Step 7: Assign Ffwe = value

```python
Ffwe = fwefit.f
```

**Verification:**
```python
assert_almost_equal(FAdti, FAfwe)
```

### Step 8: Assign MDfwe = value

```python
MDfwe = fwefit.md
```

**Verification:**
```python
assert_almost_equal(Ffwe, gtf)
```

### Step 9: Call assert_almost_equal()

```python
assert_almost_equal(FAdti, FAfwe, decimal=3)
```

**Verification:**
```python
assert_almost_equal(MDfwe, MDfwe)
```

### Step 10: Call assert_almost_equal()

```python
assert_almost_equal(Ffwe, gtf, decimal=3)
```

### Step 11: Call assert_almost_equal()

```python
assert_almost_equal(MDfwe, MDdti, decimal=3)
```

### Step 12: Assign fwdm = fwdti.FreeWaterTensorModel(...)

```python
fwdm = fwdti.FreeWaterTensorModel(gtab_2s, fit_method='NLS', cholesky=False)
```

### Step 13: Assign fwefit = fwdm.fit(...)

```python
fwefit = fwdm.fit(S_conta)
```

### Step 14: Assign FAfwe = value

```python
FAfwe = fwefit.fa
```

### Step 15: Assign Ffwe = value

```python
Ffwe = fwefit.f
```

### Step 16: Assign MDfwe = value

```python
MDfwe = fwefit.md
```

### Step 17: Call assert_almost_equal()

```python
assert_almost_equal(FAdti, FAfwe)
```

### Step 18: Call assert_almost_equal()

```python
assert_almost_equal(Ffwe, gtf)
```

### Step 19: Call assert_almost_equal()

```python
assert_almost_equal(MDfwe, MDdti)
```

### Step 20: Assign fwdm = fwdti.FreeWaterTensorModel(...)

```python
fwdm = fwdti.FreeWaterTensorModel(gtab_2s, fit_method='NLS', cholesky=True)
```

### Step 21: Assign fwefit = fwdm.fit(...)

```python
fwefit = fwdm.fit(S_conta)
```

### Step 22: Assign FAfwe = value

```python
FAfwe = fwefit.fa
```

### Step 23: Assign Ffwe = value

```python
Ffwe = fwefit.f
```

### Step 24: Assign MDfwe = value

```python
MDfwe = fwefit.md
```

### Step 25: Call assert_almost_equal()

```python
assert_almost_equal(FAdti, FAfwe)
```

### Step 26: Call assert_almost_equal()

```python
assert_almost_equal(Ffwe, gtf)
```

### Step 27: Call assert_almost_equal()

```python
assert_almost_equal(MDfwe, MDfwe)
```


## Complete Example

```python
# Workflow
gtf = 0.44444
mevals = np.array([[0.0017, 0.0003, 0.0003], [0.003, 0.003, 0.003]])
S_conta, peaks = multi_tensor(gtab_2s, mevals, S0=100, angles=[(90, 0), (90, 0)], fractions=[(1 - gtf) * 100, gtf * 100], snr=None)
fwdm = fwdti.FreeWaterTensorModel(gtab_2s, fit_method='WLS')
fwefit = fwdm.fit(S_conta)
FAfwe = fwefit.fa
Ffwe = fwefit.f
MDfwe = fwefit.md
assert_almost_equal(FAdti, FAfwe, decimal=3)
assert_almost_equal(Ffwe, gtf, decimal=3)
assert_almost_equal(MDfwe, MDdti, decimal=3)
fwdm = fwdti.FreeWaterTensorModel(gtab_2s, fit_method='NLS', cholesky=False)
fwefit = fwdm.fit(S_conta)
FAfwe = fwefit.fa
Ffwe = fwefit.f
MDfwe = fwefit.md
assert_almost_equal(FAdti, FAfwe)
assert_almost_equal(Ffwe, gtf)
assert_almost_equal(MDfwe, MDdti)
fwdm = fwdti.FreeWaterTensorModel(gtab_2s, fit_method='NLS', cholesky=True)
fwefit = fwdm.fit(S_conta)
FAfwe = fwefit.fa
Ffwe = fwefit.f
MDfwe = fwefit.md
assert_almost_equal(FAdti, FAfwe)
assert_almost_equal(Ffwe, gtf)
assert_almost_equal(MDfwe, MDfwe)
```

## Next Steps


---

*Source: test_fwdti.py:87 | Complexity: Advanced | Last updated: 2026-05-18*