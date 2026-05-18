# How To: Plot Img Comparison

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, mock, workflow, integration

## Overview

Workflow: Tests for plot_img_comparison.

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
# Fixtures: matplotlib_pyplot, rng, tmp_path
```

## Step-by-Step Guide

### Step 1: 'Tests for plot_img_comparison.'

```python
'Tests for plot_img_comparison.'
```

**Verification:**
```python
assert len(correlations) == len(query_images)
```

### Step 2: Assign unknown = plt.subplots(...)

```python
_, axes = plt.subplots(2, 1)
```

**Verification:**
```python
assert correlations[0] == pytest.approx(1.0)
```

### Step 3: Assign axes = axes.ravel(...)

```python
axes = axes.ravel()
```

**Verification:**
```python
assert len(ax_0.collections) == length
```

### Step 4: Assign length = 2

```python
length = 2
```

**Verification:**
```python
assert len(ax_0.collections[0].get_edgecolors() == masker.transform(target_images[0]).ravel().shape[0])
```

### Step 5: Assign unknown = generate_fake_fmri(...)

```python
query_images, mask_img = generate_fake_fmri(random_state=rng, shape=(2, 3, 4), length=length)
```

**Verification:**
```python
assert ax_0.get_ylabel() == 'query'
```

### Step 6: Assign query_images = list(...)

```python
query_images = list(iter_img(query_images))
```

**Verification:**
```python
assert ax_0.get_xlabel() == 'image set 1'
```

### Step 7: Assign unknown = generate_fake_fmri(...)

```python
target_images, _ = generate_fake_fmri(random_state=rng, shape=(4, 5, 6), length=length)
```

**Verification:**
```python
assert len(ax_0.lines) == length
```

### Step 8: Assign target_images = list(...)

```python
target_images = list(iter_img(target_images))
```

**Verification:**
```python
assert ax_0.lines[0].get_linestyle() == '--'
```

### Step 9: Assign unknown = value

```python
target_images[0] = query_images[0]
```

**Verification:**
```python
assert ax_1.get_title() == 'Histogram of imgs values'
```

### Step 10: Assign masker = NiftiMasker.fit(...)

```python
masker = NiftiMasker(mask_img, standardize=None).fit()
```

**Verification:**
```python
assert len(ax_1.patches) == length * 2 * gridsize
```

### Step 11: Assign correlations = plot_img_comparison(...)

```python
correlations = plot_img_comparison(target_images, query_images, masker, axes=axes, src_label='query', output_dir=tmp_path, colorbar=False)
```

**Verification:**
```python
assert len(correlations) == len(query_images)
```

### Step 12: Assign unknown = axes

```python
ax_0, ax_1 = axes
```

**Verification:**
```python
assert len(ax_0.collections) == length
```

### Step 13: Assign gridsize = 100

```python
gridsize = 100
```

**Verification:**
```python
assert len(ax_1.patches) == length * 2 * gridsize
```


## Complete Example

```python
# Setup
# Fixtures: matplotlib_pyplot, rng, tmp_path

# Workflow
'Tests for plot_img_comparison.'
_, axes = plt.subplots(2, 1)
axes = axes.ravel()
length = 2
query_images, mask_img = generate_fake_fmri(random_state=rng, shape=(2, 3, 4), length=length)
query_images = list(iter_img(query_images))
target_images, _ = generate_fake_fmri(random_state=rng, shape=(4, 5, 6), length=length)
target_images = list(iter_img(target_images))
target_images[0] = query_images[0]
masker = NiftiMasker(mask_img, standardize=None).fit()
correlations = plot_img_comparison(target_images, query_images, masker, axes=axes, src_label='query', output_dir=tmp_path, colorbar=False)
assert len(correlations) == len(query_images)
assert correlations[0] == pytest.approx(1.0)
ax_0, ax_1 = axes
assert len(ax_0.collections) == length
assert len(ax_0.collections[0].get_edgecolors() == masker.transform(target_images[0]).ravel().shape[0])
assert ax_0.get_ylabel() == 'query'
assert ax_0.get_xlabel() == 'image set 1'
assert len(ax_0.lines) == length
assert ax_0.lines[0].get_linestyle() == '--'
assert ax_1.get_title() == 'Histogram of imgs values'
gridsize = 100
assert len(ax_1.patches) == length * 2 * gridsize
```

## Next Steps


---

*Source: test_img_comparisons.py:83 | Complexity: Advanced | Last updated: 2026-05-18*