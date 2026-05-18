# How To: Plot Img Comparison Without Plot

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Tests for plot_img_comparison no plot should return same result.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `nibabel`
- `nilearn._utils.data_gen`
- `nilearn.conftest`
- `nilearn.image`
- `nilearn.maskers`
- `nilearn.plotting`

**Setup Required:**
```python
# Fixtures: matplotlib_pyplot, rng
```

## Step-by-Step Guide

### Step 1: 'Tests for plot_img_comparison no plot should return same result.'

```python
'Tests for plot_img_comparison no plot should return same result.'
```

**Verification:**
```python
assert np.allclose(correlations, correlations_1)
```

### Step 2: Assign unknown = plt.subplots(...)

```python
_, axes = plt.subplots(2, 1)
```

### Step 3: Assign axes = axes.ravel(...)

```python
axes = axes.ravel()
```

### Step 4: Assign unknown = generate_fake_fmri(...)

```python
query_images, mask_img = generate_fake_fmri(random_state=rng, shape=(2, 3, 4), length=2)
```

### Step 5: Assign query_images = list(...)

```python
query_images = list(iter_img(query_images))
```

### Step 6: Assign unknown = generate_fake_fmri(...)

```python
target_images, _ = generate_fake_fmri(random_state=rng, shape=(2, 3, 4), length=2)
```

### Step 7: Assign target_images = list(...)

```python
target_images = list(iter_img(target_images))
```

### Step 8: Assign unknown = value

```python
target_images[0] = query_images[0]
```

### Step 9: Assign masker = NiftiMasker.fit(...)

```python
masker = NiftiMasker(mask_img, standardize=None).fit()
```

### Step 10: Assign correlations = plot_img_comparison(...)

```python
correlations = plot_img_comparison(target_images, query_images, masker, plot_hist=True, colorbar=False)
```

### Step 11: Assign correlations_1 = plot_img_comparison(...)

```python
correlations_1 = plot_img_comparison(target_images, query_images, masker, plot_hist=False)
```

**Verification:**
```python
assert np.allclose(correlations, correlations_1)
```


## Complete Example

```python
# Setup
# Fixtures: matplotlib_pyplot, rng

# Workflow
'Tests for plot_img_comparison no plot should return same result.'
_, axes = plt.subplots(2, 1)
axes = axes.ravel()
query_images, mask_img = generate_fake_fmri(random_state=rng, shape=(2, 3, 4), length=2)
query_images = list(iter_img(query_images))
target_images, _ = generate_fake_fmri(random_state=rng, shape=(2, 3, 4), length=2)
target_images = list(iter_img(target_images))
target_images[0] = query_images[0]
masker = NiftiMasker(mask_img, standardize=None).fit()
correlations = plot_img_comparison(target_images, query_images, masker, plot_hist=True, colorbar=False)
correlations_1 = plot_img_comparison(target_images, query_images, masker, plot_hist=False)
assert np.allclose(correlations, correlations_1)
```

## Next Steps


---

*Source: test_img_comparisons.py:137 | Complexity: Advanced | Last updated: 2026-05-18*