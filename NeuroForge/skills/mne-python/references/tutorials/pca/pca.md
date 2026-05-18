# How To: Pca

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test PCA equivalence.

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
# Fixtures: n_components, whiten
```

## Step-by-Step Guide

### Step 1: 'Test PCA equivalence.'

```python
'Test PCA equivalence.'
```

**Verification:**
```python
assert_array_equal(X, X_orig)
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('sklearn')
```

**Verification:**
```python
assert_array_equal(X, X_orig)
```

### Step 3: Assign unknown = value

```python
n_samples, n_dim = (1000, 10)
```

**Verification:**
```python
assert_allclose(X_skl, X_mne * np.sign(np.sum(X_skl * X_mne, axis=0)))
```

### Step 4: Assign X = np.random.RandomState.randn(...)

```python
X = np.random.RandomState(0).randn(n_samples, n_dim)
```

**Verification:**
```python
assert pca_mne.n_components_ == pca_skl.n_components_
```

### Step 5: Assign unknown = np.mean(...)

```python
X[:, -1] = np.mean(X[:, :-1], axis=-1)
```

**Verification:**
```python
assert_allclose(val_skl, val_mne)
```

### Step 6: Assign X_orig = X.copy(...)

```python
X_orig = X.copy()
```

**Verification:**
```python
assert pca_mne.n_components_ == n_dim - 1
```

### Step 7: Assign pca_skl = PCA(...)

```python
pca_skl = PCA(n_components, whiten=whiten, svd_solver='full')
```

**Verification:**
```python
assert pca_mne.n_components_ == n_components
```

### Step 8: Assign pca_mne = _PCA(...)

```python
pca_mne = _PCA(n_components, whiten=whiten)
```

**Verification:**
```python
assert pca_mne.n_components_ == n_dim - 1
```

### Step 9: Assign X_skl = pca_skl.fit_transform(...)

```python
X_skl = pca_skl.fit_transform(X)
```

**Verification:**
```python
assert n_components is None
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(X, X_orig)
```

**Verification:**
```python
assert pca_mne.n_components_ == n_dim
```

### Step 11: Assign X_mne = pca_mne.fit_transform(...)

```python
X_mne = pca_mne.fit_transform(X)
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(X, X_orig)
```

### Step 13: Call assert_allclose()

```python
assert_allclose(X_skl, X_mne * np.sign(np.sum(X_skl * X_mne, axis=0)))
```

**Verification:**
```python
assert pca_mne.n_components_ == pca_skl.n_components_
```

### Step 14: Assign unknown = value

```python
val_skl, val_mne = (getattr(pca_skl, key), getattr(pca_mne, key))
```

### Step 15: Call assert_allclose()

```python
assert_allclose(val_skl, val_mne)
```

**Verification:**
```python
assert pca_mne.n_components_ == n_dim - 1
```

### Step 16: Assign val_mne = value

```python
val_mne = val_mne * np.sign(np.sum(val_skl * val_mne, axis=1, keepdims=True))
```

**Verification:**
```python
assert pca_mne.n_components_ == n_components
```


## Complete Example

```python
# Setup
# Fixtures: n_components, whiten

# Workflow
'Test PCA equivalence.'
pytest.importorskip('sklearn')
from sklearn.decomposition import PCA
n_samples, n_dim = (1000, 10)
X = np.random.RandomState(0).randn(n_samples, n_dim)
X[:, -1] = np.mean(X[:, :-1], axis=-1)
X_orig = X.copy()
pca_skl = PCA(n_components, whiten=whiten, svd_solver='full')
pca_mne = _PCA(n_components, whiten=whiten)
X_skl = pca_skl.fit_transform(X)
assert_array_equal(X, X_orig)
X_mne = pca_mne.fit_transform(X)
assert_array_equal(X, X_orig)
assert_allclose(X_skl, X_mne * np.sign(np.sum(X_skl * X_mne, axis=0)))
assert pca_mne.n_components_ == pca_skl.n_components_
for key in ('mean_', 'components_', 'explained_variance_', 'explained_variance_ratio_'):
    val_skl, val_mne = (getattr(pca_skl, key), getattr(pca_mne, key))
    if key == 'components_':
        val_mne = val_mne * np.sign(np.sum(val_skl * val_mne, axis=1, keepdims=True))
    assert_allclose(val_skl, val_mne)
if isinstance(n_components, float):
    assert pca_mne.n_components_ == n_dim - 1
elif isinstance(n_components, int):
    assert pca_mne.n_components_ == n_components
elif n_components == 'mle':
    assert pca_mne.n_components_ == n_dim - 1
else:
    assert n_components is None
    assert pca_mne.n_components_ == n_dim
```

## Next Steps


---

*Source: test_numerics.py:439 | Complexity: Advanced | Last updated: 2026-05-18*