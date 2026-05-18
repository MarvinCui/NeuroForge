# How To: Multi Pca

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Components are the same if we put twice the same data,        and that fit output is deterministic.
    

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
# Fixtures: length, data_type, decomposition_mask_img, decomposition_images
```

## Step-by-Step Guide

### Step 1: 'Components are the same if we put twice the same data,        and that fit output is deterministic.\n    '

```python
'Components are the same if we put twice the same data,        and that fit output is deterministic.\n    '
```

**Verification:**
```python
assert_array_equal(components1, components2)
```

### Step 2: Assign multi_pca = _MultiPCA(...)

```python
multi_pca = _MultiPCA(mask=decomposition_mask_img, n_components=3, random_state=RANDOM_STATE, standardize='zscore_sample')
```

**Verification:**
```python
assert_array_almost_equal(components1, components2)
```

### Step 3: Call multi_pca.fit()

```python
multi_pca.fit(decomposition_images)
```

### Step 4: Call check_decomposition_estimator()

```python
check_decomposition_estimator(multi_pca, data_type)
```

### Step 5: Assign components1 = value

```python
components1 = multi_pca.components_
```

### Step 6: Assign multi_pca = _MultiPCA(...)

```python
multi_pca = _MultiPCA(mask=decomposition_mask_img, n_components=3, random_state=RANDOM_STATE, standardize='zscore_sample')
```

### Step 7: Call multi_pca.fit()

```python
multi_pca.fit(length * decomposition_images)
```

### Step 8: Assign components2 = value

```python
components2 = multi_pca.components_
```

### Step 9: Call assert_array_equal()

```python
assert_array_equal(components1, components2)
```

### Step 10: Call assert_array_almost_equal()

```python
assert_array_almost_equal(components1, components2)
```


## Complete Example

```python
# Setup
# Fixtures: length, data_type, decomposition_mask_img, decomposition_images

# Workflow
'Components are the same if we put twice the same data,        and that fit output is deterministic.\n    '
multi_pca = _MultiPCA(mask=decomposition_mask_img, n_components=3, random_state=RANDOM_STATE, standardize='zscore_sample')
multi_pca.fit(decomposition_images)
check_decomposition_estimator(multi_pca, data_type)
components1 = multi_pca.components_
multi_pca = _MultiPCA(mask=decomposition_mask_img, n_components=3, random_state=RANDOM_STATE, standardize='zscore_sample')
multi_pca.fit(length * decomposition_images)
components2 = multi_pca.components_
if length == 1:
    assert_array_equal(components1, components2)
else:
    assert_array_almost_equal(components1, components2)
```

## Next Steps


---

*Source: test_multi_pca.py:22 | Complexity: Advanced | Last updated: 2026-05-18*