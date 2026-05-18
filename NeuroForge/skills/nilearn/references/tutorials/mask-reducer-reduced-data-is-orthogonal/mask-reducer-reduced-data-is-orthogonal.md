# How To: Mask Reducer Reduced Data Is Orthogonal

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test that the reduced data is orthogonal.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `nilearn.conftest`
- `nilearn.decomposition._base`
- `nilearn.decomposition.tests.conftest`

**Setup Required:**
```python
# Fixtures: data_type, decomposition_masker, decomposition_img
```

## Step-by-Step Guide

### Step 1: 'Test that the reduced data is orthogonal.'

```python
'Test that the reduced data is orthogonal.'
```

**Verification:**
```python
assert data.shape == (n_components, np.prod(decomposition_masker.mask_img_.shape))
```

### Step 2: Assign n_components = 3

```python
n_components = 3
```

**Verification:**
```python
assert data.shape == (n_components, decomposition_masker.mask_img_.shape[-1])
```

### Step 3: Assign data = _mask_and_reduce(...)

```python
data = _mask_and_reduce(masker=decomposition_masker, imgs=decomposition_img, n_components=n_components, random_state=RANDOM_STATE)
```

**Verification:**
```python
assert_array_almost_equal(cov, cov_diag)
```

### Step 4: Assign cov = data.dot(...)

```python
cov = data.dot(data.T)
```

### Step 5: Assign cov_diag = np.zeros(...)

```python
cov_diag = np.zeros((3, 3))
```

### Step 6: Call assert_array_almost_equal()

```python
assert_array_almost_equal(cov, cov_diag)
```

**Verification:**
```python
assert data.shape == (n_components, np.prod(decomposition_masker.mask_img_.shape))
```

### Step 7: Assign unknown = value

```python
cov_diag[i, i] = cov[i, i]
```

**Verification:**
```python
assert data.shape == (n_components, decomposition_masker.mask_img_.shape[-1])
```


## Complete Example

```python
# Setup
# Fixtures: data_type, decomposition_masker, decomposition_img

# Workflow
'Test that the reduced data is orthogonal.'
n_components = 3
data = _mask_and_reduce(masker=decomposition_masker, imgs=decomposition_img, n_components=n_components, random_state=RANDOM_STATE)
if data_type == 'nifti':
    assert data.shape == (n_components, np.prod(decomposition_masker.mask_img_.shape))
elif data_type == 'surface':
    assert data.shape == (n_components, decomposition_masker.mask_img_.shape[-1])
cov = data.dot(data.T)
cov_diag = np.zeros((3, 3))
for i in range(3):
    cov_diag[i, i] = cov[i, i]
assert_array_almost_equal(cov, cov_diag)
```

## Next Steps


---

*Source: test_base.py:133 | Complexity: Intermediate | Last updated: 2026-05-18*