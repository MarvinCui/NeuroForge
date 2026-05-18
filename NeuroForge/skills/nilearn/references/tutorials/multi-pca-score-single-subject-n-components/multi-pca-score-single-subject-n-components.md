# How To: Multi Pca Score Single Subject N Components

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Score is one for n_components == n_sample        in single subject configuration.
    

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `nilearn.decomposition._multi_pca`
- `nilearn.decomposition.tests.conftest`
- `nilearn.maskers`

**Setup Required:**
```python
# Fixtures: data_type, decomposition_mask_img, decomposition_img, with_activation
```

## Step-by-Step Guide

### Step 1: 'Score is one for n_components == n_sample        in single subject configuration.\n    '

```python
'Score is one for n_components == n_sample        in single subject configuration.\n    '
```

**Verification:**
```python
assert_almost_equal(s, 1.0, 1)
```

### Step 2: Assign multi_pca = _MultiPCA(...)

```python
multi_pca = _MultiPCA(mask=decomposition_mask_img, random_state=RANDOM_STATE, memory_level=0, n_components=5, standardize='zscore_sample')
```

**Verification:**
```python
assert s.shape == (5,)
```

### Step 3: Call multi_pca.fit()

```python
multi_pca.fit(decomposition_img)
```

**Verification:**
```python
assert np.all(s <= 1)
```

### Step 4: Call check_decomposition_estimator()

```python
check_decomposition_estimator(multi_pca, data_type)
```

**Verification:**
```python
assert np.all(s >= 0)
```

### Step 5: Assign s = multi_pca.score(...)

```python
s = multi_pca.score(decomposition_img)
```

### Step 6: Call assert_almost_equal()

```python
assert_almost_equal(s, 1.0, 1)
```

### Step 7: Assign s = multi_pca._raw_score(...)

```python
s = multi_pca._raw_score(masker.transform(decomposition_img), per_component=True)
```

**Verification:**
```python
assert s.shape == (5,)
```

### Step 8: Assign masker = NiftiMasker.fit(...)

```python
masker = NiftiMasker(decomposition_mask_img, standardize=None).fit()
```

### Step 9: Assign masker = SurfaceMasker.fit(...)

```python
masker = SurfaceMasker(decomposition_mask_img, standardize=None).fit()
```


## Complete Example

```python
# Setup
# Fixtures: data_type, decomposition_mask_img, decomposition_img, with_activation

# Workflow
'Score is one for n_components == n_sample        in single subject configuration.\n    '
multi_pca = _MultiPCA(mask=decomposition_mask_img, random_state=RANDOM_STATE, memory_level=0, n_components=5, standardize='zscore_sample')
multi_pca.fit(decomposition_img)
check_decomposition_estimator(multi_pca, data_type)
s = multi_pca.score(decomposition_img)
assert_almost_equal(s, 1.0, 1)
if data_type == 'nifti':
    masker = NiftiMasker(decomposition_mask_img, standardize=None).fit()
elif data_type == 'surface':
    masker = SurfaceMasker(decomposition_mask_img, standardize=None).fit()
s = multi_pca._raw_score(masker.transform(decomposition_img), per_component=True)
assert s.shape == (5,)
assert np.all(s <= 1)
assert np.all(s >= 0)
```

## Next Steps


---

*Source: test_multi_pca.py:85 | Complexity: Advanced | Last updated: 2026-05-18*