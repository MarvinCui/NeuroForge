# How To: Multi Tensor

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test multi tensor

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

### Step 1: Assign mevals = np.array(...)

```python
mevals = np.array(([0.0015, 0.0003, 0.0003], [0.0015, 0.0003, 0.0003]))
```

**Verification:**
```python
assert_array_almost_equal(S, Ssingle)
```

### Step 2: Assign e0 = np.array(...)

```python
e0 = np.array([np.sqrt(2) / 2.0, np.sqrt(2) / 2.0, 0])
```

### Step 3: Assign e1 = np.array(...)

```python
e1 = np.array([0, np.sqrt(2) / 2.0, np.sqrt(2) / 2.0])
```

### Step 4: Assign mevecs = value

```python
mevecs = [all_tensor_evecs(e0), all_tensor_evecs(e1)]
```

### Step 5: Assign unknown = get_fnames(...)

```python
fimg, fbvals, fbvecs = get_fnames(name='small_101D')
```

### Step 6: Assign unknown = read_bvals_bvecs(...)

```python
bvals, bvecs = read_bvals_bvecs(fbvals, fbvecs)
```

### Step 7: Assign gtab = gradient_table(...)

```python
gtab = gradient_table(bvals, bvecs=bvecs)
```

### Step 8: Assign s1 = single_tensor(...)

```python
s1 = single_tensor(gtab, 100, evals=mevals[0], evecs=mevecs[0], snr=None)
```

### Step 9: Assign s2 = single_tensor(...)

```python
s2 = single_tensor(gtab, 100, evals=mevals[1], evecs=mevecs[1], snr=None)
```

### Step 10: Assign Ssingle = value

```python
Ssingle = 0.5 * s1 + 0.5 * s2
```

### Step 11: Assign unknown = multi_tensor(...)

```python
S, _ = multi_tensor(gtab, mevals, S0=100, angles=[(90, 45), (45, 90)], fractions=[50, 50], snr=None)
```

### Step 12: Call assert_array_almost_equal()

```python
assert_array_almost_equal(S, Ssingle)
```


## Complete Example

```python
# Workflow
mevals = np.array(([0.0015, 0.0003, 0.0003], [0.0015, 0.0003, 0.0003]))
e0 = np.array([np.sqrt(2) / 2.0, np.sqrt(2) / 2.0, 0])
e1 = np.array([0, np.sqrt(2) / 2.0, np.sqrt(2) / 2.0])
mevecs = [all_tensor_evecs(e0), all_tensor_evecs(e1)]
fimg, fbvals, fbvecs = get_fnames(name='small_101D')
bvals, bvecs = read_bvals_bvecs(fbvals, fbvecs)
gtab = gradient_table(bvals, bvecs=bvecs)
s1 = single_tensor(gtab, 100, evals=mevals[0], evecs=mevecs[0], snr=None)
s2 = single_tensor(gtab, 100, evals=mevals[1], evecs=mevecs[1], snr=None)
Ssingle = 0.5 * s1 + 0.5 * s2
S, _ = multi_tensor(gtab, mevals, S0=100, angles=[(90, 45), (45, 90)], fractions=[50, 50], snr=None)
assert_array_almost_equal(S, Ssingle)
```

## Next Steps


---

*Source: test_voxel.py:133 | Complexity: Advanced | Last updated: 2026-05-18*