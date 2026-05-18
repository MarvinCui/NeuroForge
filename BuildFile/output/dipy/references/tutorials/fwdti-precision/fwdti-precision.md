# How To: Fwdti Precision

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test fwdti precision

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

### Step 1: Assign gtf = 0.63416

```python
gtf = 0.63416
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
assert_almost_equal(MDfwe, MDdti, decimal=5)
```

### Step 4: Assign fwdm = fwdti.FreeWaterTensorModel(...)

```python
fwdm = fwdti.FreeWaterTensorModel(gtab_2s, fit_method='WLS', piterations=5)
```

### Step 5: Assign fwefit = fwdm.fit(...)

```python
fwefit = fwdm.fit(S_conta)
```

### Step 6: Assign FAfwe = value

```python
FAfwe = fwefit.fa
```

### Step 7: Assign Ffwe = value

```python
Ffwe = fwefit.f
```

### Step 8: Assign MDfwe = value

```python
MDfwe = fwefit.md
```

### Step 9: Call assert_almost_equal()

```python
assert_almost_equal(FAdti, FAfwe, decimal=3)
```

### Step 10: Call assert_almost_equal()

```python
assert_almost_equal(Ffwe, gtf, decimal=3)
```

### Step 11: Call assert_almost_equal()

```python
assert_almost_equal(MDfwe, MDdti, decimal=5)
```


## Complete Example

```python
# Workflow
gtf = 0.63416
mevals = np.array([[0.0017, 0.0003, 0.0003], [0.003, 0.003, 0.003]])
S_conta, peaks = multi_tensor(gtab_2s, mevals, S0=100, angles=[(90, 0), (90, 0)], fractions=[(1 - gtf) * 100, gtf * 100], snr=None)
fwdm = fwdti.FreeWaterTensorModel(gtab_2s, fit_method='WLS', piterations=5)
fwefit = fwdm.fit(S_conta)
FAfwe = fwefit.fa
Ffwe = fwefit.f
MDfwe = fwefit.md
assert_almost_equal(FAdti, FAfwe, decimal=3)
assert_almost_equal(Ffwe, gtf, decimal=3)
assert_almost_equal(MDfwe, MDdti, decimal=5)
```

## Next Steps


---

*Source: test_fwdti.py:132 | Complexity: Advanced | Last updated: 2026-05-18*