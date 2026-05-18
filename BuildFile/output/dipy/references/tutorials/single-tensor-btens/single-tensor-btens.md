# How To: Single Tensor Btens

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Testing single tensor simulations when a btensor is given

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.data`
- `dipy.io.gradients`
- `dipy.sims.voxel`
- `dipy.testing.decorators`
- `dipy.reconst.dti`


## Step-by-Step Guide

### Step 1: 'Testing single tensor simulations when a btensor is given'

```python
'Testing single tensor simulations when a btensor is given'
```

**Verification:**
```python
assert_array_almost_equal(S_ref, S_btens)
```

### Step 2: Assign gtab_lte = gradient_table(...)

```python
gtab_lte = gradient_table(gtab.bvals, bvecs=gtab.bvecs, btens='LTE')
```

**Verification:**
```python
assert_array_almost_equal(S_ref, S_btens)
```

### Step 3: Assign gtab_ste = gradient_table(...)

```python
gtab_ste = gradient_table(gtab.bvals, bvecs=gtab.bvecs, btens='STE')
```

### Step 4: Assign evecs = np.eye(...)

```python
evecs = np.eye(3)
```

### Step 5: Assign evals = value

```python
evals = np.array([1.4, 0.35, 0.35]) * 10 ** (-3)
```

### Step 6: Assign S_ref = single_tensor(...)

```python
S_ref = single_tensor(gtab, 100, evals=evals, evecs=evecs, snr=None)
```

### Step 7: Assign S_btens = single_tensor(...)

```python
S_btens = single_tensor(gtab_lte, 100, evals=evals, evecs=evecs, snr=None)
```

### Step 8: Call assert_array_almost_equal()

```python
assert_array_almost_equal(S_ref, S_btens)
```

### Step 9: Assign md = value

```python
md = np.sum(evals) / 3
```

### Step 10: Assign S_ref = value

```python
S_ref = 100 * np.exp(-gtab.bvals * md)
```

### Step 11: Assign S_btens = single_tensor(...)

```python
S_btens = single_tensor(gtab_ste, 100, evals=evals, evecs=evecs, snr=None)
```

### Step 12: Call assert_array_almost_equal()

```python
assert_array_almost_equal(S_ref, S_btens)
```


## Complete Example

```python
# Workflow
'Testing single tensor simulations when a btensor is given'
gtab_lte = gradient_table(gtab.bvals, bvecs=gtab.bvecs, btens='LTE')
gtab_ste = gradient_table(gtab.bvals, bvecs=gtab.bvecs, btens='STE')
evecs = np.eye(3)
evals = np.array([1.4, 0.35, 0.35]) * 10 ** (-3)
S_ref = single_tensor(gtab, 100, evals=evals, evecs=evecs, snr=None)
S_btens = single_tensor(gtab_lte, 100, evals=evals, evecs=evecs, snr=None)
assert_array_almost_equal(S_ref, S_btens)
md = np.sum(evals) / 3
S_ref = 100 * np.exp(-gtab.bvals * md)
S_btens = single_tensor(gtab_ste, 100, evals=evals, evecs=evecs, snr=None)
assert_array_almost_equal(S_ref, S_btens)
```

## Next Steps


---

*Source: test_voxel.py:388 | Complexity: Advanced | Last updated: 2026-05-18*