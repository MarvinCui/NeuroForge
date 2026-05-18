# How To: Md Regularization

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test md regularization

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

### Step 1: Assign gtf = 0.97

```python
gtf = 0.97
```

**Verification:**
```python
assert_array_almost_equal(fwefit.fa, 0.0)
```

### Step 2: Assign mevals = np.array(...)

```python
mevals = np.array([[0.0017, 0.0003, 0.0003], [0.003, 0.003, 0.003]])
```

**Verification:**
```python
assert_array_almost_equal(fwefit.md, 0.0)
```

### Step 3: Assign unknown = multi_tensor(...)

```python
S_conta, peaks = multi_tensor(gtab_2s, mevals, S0=100, angles=[(90, 0), (90, 0)], fractions=[(1 - gtf) * 100, gtf * 100], snr=None)
```

**Verification:**
```python
assert_array_almost_equal(fwefit.f, 1.0)
```

### Step 4: Assign fwdm = fwdti.FreeWaterTensorModel(...)

```python
fwdm = fwdti.FreeWaterTensorModel(gtab_2s, fit_method='NLS')
```

**Verification:**
```python
assert_array_almost_equal(fwefit.fa, FAref)
```

### Step 5: Assign fwefit = fwdm.fit(...)

```python
fwefit = fwdm.fit(S_conta)
```

**Verification:**
```python
assert_array_almost_equal(fwefit.md, MDref)
```

### Step 6: Call assert_array_almost_equal()

```python
assert_array_almost_equal(fwefit.fa, 0.0)
```

**Verification:**
```python
assert_array_almost_equal(fwefit.f, GTF)
```

### Step 7: Call assert_array_almost_equal()

```python
assert_array_almost_equal(fwefit.md, 0.0)
```

### Step 8: Call assert_array_almost_equal()

```python
assert_array_almost_equal(fwefit.f, 1.0)
```

### Step 9: Assign unknown = S_conta

```python
DWI[0, 1, 1] = S_conta
```

### Step 10: Assign unknown = 1

```python
GTF[0, 1, 1] = 1
```

### Step 11: Assign unknown = 0

```python
FAref[0, 1, 1] = 0
```

### Step 12: Assign unknown = 0

```python
MDref[0, 1, 1] = 0
```

### Step 13: Assign fwefit = fwdm.fit(...)

```python
fwefit = fwdm.fit(DWI)
```

### Step 14: Call assert_array_almost_equal()

```python
assert_array_almost_equal(fwefit.fa, FAref)
```

### Step 15: Call assert_array_almost_equal()

```python
assert_array_almost_equal(fwefit.md, MDref)
```

### Step 16: Call assert_array_almost_equal()

```python
assert_array_almost_equal(fwefit.f, GTF)
```


## Complete Example

```python
# Workflow
gtf = 0.97
mevals = np.array([[0.0017, 0.0003, 0.0003], [0.003, 0.003, 0.003]])
S_conta, peaks = multi_tensor(gtab_2s, mevals, S0=100, angles=[(90, 0), (90, 0)], fractions=[(1 - gtf) * 100, gtf * 100], snr=None)
fwdm = fwdti.FreeWaterTensorModel(gtab_2s, fit_method='NLS')
fwefit = fwdm.fit(S_conta)
assert_array_almost_equal(fwefit.fa, 0.0)
assert_array_almost_equal(fwefit.md, 0.0)
assert_array_almost_equal(fwefit.f, 1.0)
DWI[0, 1, 1] = S_conta
GTF[0, 1, 1] = 1
FAref[0, 1, 1] = 0
MDref[0, 1, 1] = 0
fwefit = fwdm.fit(DWI)
assert_array_almost_equal(fwefit.fa, FAref)
assert_array_almost_equal(fwefit.md, MDref)
assert_array_almost_equal(fwefit.f, GTF)
```

## Next Steps


---

*Source: test_fwdti.py:311 | Complexity: Advanced | Last updated: 2026-05-18*