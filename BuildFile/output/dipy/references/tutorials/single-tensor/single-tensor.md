# How To: Single Tensor

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test single tensor

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

### Step 1: Assign evals = value

```python
evals = np.array([1.4, 0.35, 0.35]) * 10 ** (-3)
```

**Verification:**
```python
assert_array_almost_equal(S[gtab.b0s_mask], 100)
```

### Step 2: Assign evecs = np.eye(...)

```python
evecs = np.eye(3)
```

**Verification:**
```python
assert_(np.mean(S[~gtab.b0s_mask]) < 100)
```

### Step 3: Assign S = single_tensor(...)

```python
S = single_tensor(gtab, 100, evals=evals, evecs=evecs, snr=None)
```

**Verification:**
```python
assert_array_almost_equal(t.fa, 0.707, decimal=3)
```

### Step 4: Call assert_array_almost_equal()

```python
assert_array_almost_equal(S[gtab.b0s_mask], 100)
```

### Step 5: Call assert_()

```python
assert_(np.mean(S[~gtab.b0s_mask]) < 100)
```

### Step 6: Assign m = TensorModel(...)

```python
m = TensorModel(gtab)
```

### Step 7: Assign t = m.fit(...)

```python
t = m.fit(S)
```

### Step 8: Call assert_array_almost_equal()

```python
assert_array_almost_equal(t.fa, 0.707, decimal=3)
```


## Complete Example

```python
# Workflow
evals = np.array([1.4, 0.35, 0.35]) * 10 ** (-3)
evecs = np.eye(3)
S = single_tensor(gtab, 100, evals=evals, evecs=evecs, snr=None)
assert_array_almost_equal(S[gtab.b0s_mask], 100)
assert_(np.mean(S[~gtab.b0s_mask]) < 100)
from dipy.reconst.dti import TensorModel
m = TensorModel(gtab)
t = m.fit(S)
assert_array_almost_equal(t.fa, 0.707, decimal=3)
```

## Next Steps


---

*Source: test_voxel.py:118 | Complexity: Advanced | Last updated: 2026-05-18*