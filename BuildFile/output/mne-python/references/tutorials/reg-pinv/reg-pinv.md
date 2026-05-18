# How To: Reg Pinv

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test regularization and inversion of covariance matrix.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `copy`
- `datetime`
- `io`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.pick`
- `mne.epochs`
- `mne.fixes`
- `mne.io`
- `mne.time_frequency`
- `mne.utils`
- `mne.utils.numerics`
- `sklearn.decomposition`

**Setup Required:**
```python
# Fixtures: ndim
```

## Step-by-Step Guide

### Step 1: 'Test regularization and inversion of covariance matrix.'

```python
'Test regularization and inversion of covariance matrix.'
```

**Verification:**
```python
assert loading_factor == 0
```

### Step 2: Assign a = np.array(...)

```python
a = np.array([[1.0, 0.0, 1.0], [0.0, 1.0, 0.0], [1.0, 0.0, 1.0]])
```

**Verification:**
```python
assert rank == 2
```

### Step 3: Assign a_inv_np = np.linalg.pinv(...)

```python
a_inv_np = np.linalg.pinv(a, hermitian=True)
```

**Verification:**
```python
assert_allclose(a_inv_np, a_inv_mne, atol=1e-14)
```

### Step 4: Assign unknown = _reg_pinv(...)

```python
a_inv_mne, loading_factor, rank = _reg_pinv(a, rank=2)
```

**Verification:**
```python
assert_allclose(a_inv_np, a_inv_mne, atol=1e-14)
```

### Step 5: Call assert_allclose()

```python
assert_allclose(a_inv_np, a_inv_mne, atol=1e-14)
```

**Verification:**
```python
assert estimated_rank == 2
```

### Step 6: Assign unknown = _reg_pinv(...)

```python
a_inv_mne, _, estimated_rank = _reg_pinv(a, rank=None)
```

**Verification:**
```python
assert loading_factor == 2
```

### Step 7: Call assert_allclose()

```python
assert_allclose(a_inv_np, a_inv_mne, atol=1e-14)
```

**Verification:**
```python
assert estimated_rank == 2
```

### Step 8: Assign unknown = _reg_pinv(...)

```python
a_inv_mne, loading_factor, estimated_rank = _reg_pinv(a, reg=2)
```

**Verification:**
```python
assert_allclose(a_inv_np, a_inv_mne, atol=1e-14)
```

### Step 9: Assign a_inv_np = np.linalg.pinv(...)

```python
a_inv_np = np.linalg.pinv(a + loading_factor * np.eye(3), hermitian=True)
```

**Verification:**
```python
assert_allclose(a_inv_np, a_inv_mne, atol=1e-14)
```

### Step 10: Call assert_allclose()

```python
assert_allclose(a_inv_np, a_inv_mne, atol=1e-14)
```

**Verification:**
```python
assert estimated_rank == 1
```

### Step 11: Assign a_inv_np = np.linalg.pinv(...)

```python
a_inv_np = np.linalg.pinv(a, rcond=0.5)
```

**Verification:**
```python
assert_array_equal(a_inv, 0)
```

### Step 12: Assign unknown = _reg_pinv(...)

```python
a_inv_mne, _, estimated_rank = _reg_pinv(a, rcond=0.5)
```

**Verification:**
```python
assert loading_factor == 0
```

### Step 13: Call assert_allclose()

```python
assert_allclose(a_inv_np, a_inv_mne, atol=1e-14)
```

**Verification:**
```python
assert estimated_rank == 0
```

### Step 14: Assign unknown = _reg_pinv(...)

```python
a_inv, loading_factor, estimated_rank = _reg_pinv(np.zeros((3, 3)), reg=2)
```

### Step 15: Call assert_array_equal()

```python
assert_array_equal(a_inv, 0)
```

**Verification:**
```python
assert loading_factor == 0
```

### Step 16: Assign a = value

```python
a = a[np.newaxis]
```

### Step 17: Call _reg_pinv()

```python
_reg_pinv(a, reg=0.0)
```


## Complete Example

```python
# Setup
# Fixtures: ndim

# Workflow
'Test regularization and inversion of covariance matrix.'
a = np.array([[1.0, 0.0, 1.0], [0.0, 1.0, 0.0], [1.0, 0.0, 1.0]])
for _ in range(ndim - 2):
    a = a[np.newaxis]
with pytest.warns(RuntimeWarning, match='deficient'):
    _reg_pinv(a, reg=0.0)
a_inv_np = np.linalg.pinv(a, hermitian=True)
a_inv_mne, loading_factor, rank = _reg_pinv(a, rank=2)
assert loading_factor == 0
assert rank == 2
assert_allclose(a_inv_np, a_inv_mne, atol=1e-14)
a_inv_mne, _, estimated_rank = _reg_pinv(a, rank=None)
assert_allclose(a_inv_np, a_inv_mne, atol=1e-14)
assert estimated_rank == 2
a_inv_mne, loading_factor, estimated_rank = _reg_pinv(a, reg=2)
assert loading_factor == 2
assert estimated_rank == 2
a_inv_np = np.linalg.pinv(a + loading_factor * np.eye(3), hermitian=True)
assert_allclose(a_inv_np, a_inv_mne, atol=1e-14)
a_inv_np = np.linalg.pinv(a, rcond=0.5)
a_inv_mne, _, estimated_rank = _reg_pinv(a, rcond=0.5)
assert_allclose(a_inv_np, a_inv_mne, atol=1e-14)
assert estimated_rank == 1
a_inv, loading_factor, estimated_rank = _reg_pinv(np.zeros((3, 3)), reg=2)
assert_array_equal(a_inv, 0)
assert loading_factor == 0
assert estimated_rank == 0
```

## Next Steps


---

*Source: test_numerics.py:257 | Complexity: Advanced | Last updated: 2026-05-18*