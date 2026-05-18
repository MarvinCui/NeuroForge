# How To: Smt2 Specific Cases

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test smt2 specific cases

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

### Step 1: Assign mdkiM = msdki.MeanDiffusionKurtosisModel(...)

```python
mdkiM = msdki.MeanDiffusionKurtosisModel(gtab_3s)
```

**Verification:**
```python
assert_almost_equal(mdkiF.msk, 0.0)
```

### Step 2: Assign sig_gaussian = single_tensor(...)

```python
sig_gaussian = single_tensor(gtab_3s, evals=np.array([0.002, 0.002, 0.002]))
```

**Verification:**
```python
assert_almost_equal(mdkiF.msd, 0.002)
```

### Step 3: Assign mdkiF = mdkiM.fit(...)

```python
mdkiF = mdkiM.fit(sig_gaussian)
```

**Verification:**
```python
assert_almost_equal(mdkiF.smt2f, 0)
```

### Step 4: Call assert_almost_equal()

```python
assert_almost_equal(mdkiF.msk, 0.0)
```

**Verification:**
```python
assert_almost_equal(mdkiF.smt2di, 0.002)
```

### Step 5: Call assert_almost_equal()

```python
assert_almost_equal(mdkiF.msd, 0.002)
```

**Verification:**
```python
assert_almost_equal(mdkiF.msk, 2.4, decimal=1)
```

### Step 6: Call assert_almost_equal()

```python
assert_almost_equal(mdkiF.smt2f, 0)
```

**Verification:**
```python
assert_almost_equal(mdkiF.msd * 1000, Da / 3 * 1000, decimal=1)
```

### Step 7: Call assert_almost_equal()

```python
assert_almost_equal(mdkiF.smt2di, 0.002)
```

**Verification:**
```python
assert_almost_equal(mdkiF.smt2f, 1, decimal=1)
```

### Step 8: Assign Da = 0.002

```python
Da = 0.002
```

**Verification:**
```python
assert_almost_equal(mdkiF.smt2di, mdkiF.msd * 3, decimal=1)
```

### Step 9: Assign mevals = np.zeros(...)

```python
mevals = np.zeros((64, 3))
```

### Step 10: Assign unknown = Da

```python
mevals[:, 0] = Da
```

### Step 11: Assign fracs = value

```python
fracs = np.ones(64) * 100 / 64
```

### Step 12: Assign unknown = multi_tensor_dki(...)

```python
signal_pa, dt_sph, kt_sph = multi_tensor_dki(gtab_3s, mevals, angles=bvecs[1:, :], fractions=fracs, snr=None)
```

### Step 13: Assign mdkiF = mdkiM.fit(...)

```python
mdkiF = mdkiM.fit(signal_pa)
```

### Step 14: Call assert_almost_equal()

```python
assert_almost_equal(mdkiF.msk, 2.4, decimal=1)
```

### Step 15: Call assert_almost_equal()

```python
assert_almost_equal(mdkiF.msd * 1000, Da / 3 * 1000, decimal=1)
```

### Step 16: Call assert_almost_equal()

```python
assert_almost_equal(mdkiF.smt2f, 1, decimal=1)
```

### Step 17: Call assert_almost_equal()

```python
assert_almost_equal(mdkiF.smt2di, mdkiF.msd * 3, decimal=1)
```


## Complete Example

```python
# Workflow
mdkiM = msdki.MeanDiffusionKurtosisModel(gtab_3s)
sig_gaussian = single_tensor(gtab_3s, evals=np.array([0.002, 0.002, 0.002]))
mdkiF = mdkiM.fit(sig_gaussian)
assert_almost_equal(mdkiF.msk, 0.0)
assert_almost_equal(mdkiF.msd, 0.002)
assert_almost_equal(mdkiF.smt2f, 0)
assert_almost_equal(mdkiF.smt2di, 0.002)
Da = 0.002
mevals = np.zeros((64, 3))
mevals[:, 0] = Da
fracs = np.ones(64) * 100 / 64
signal_pa, dt_sph, kt_sph = multi_tensor_dki(gtab_3s, mevals, angles=bvecs[1:, :], fractions=fracs, snr=None)
mdkiF = mdkiM.fit(signal_pa)
assert_almost_equal(mdkiF.msk, 2.4, decimal=1)
assert_almost_equal(mdkiF.msd * 1000, Da / 3 * 1000, decimal=1)
assert_almost_equal(mdkiF.smt2f, 1, decimal=1)
assert_almost_equal(mdkiF.smt2di, mdkiF.msd * 3, decimal=1)
```

## Next Steps


---

*Source: test_msdki.py:292 | Complexity: Advanced | Last updated: 2026-05-18*