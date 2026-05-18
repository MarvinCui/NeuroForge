# How To: Glm Fit Valid Mask Img

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Run fit on FLM with different valid masks.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `itertools`
- `string`
- `unittest.mock`
- `warnings`
- `pathlib`
- `numpy`
- `pandas`
- `pytest`
- `nibabel`
- `numpy.testing`
- `sklearn.cluster`
- `sklearn.utils.estimator_checks`
- `nilearn`
- `nilearn._utils.data_gen`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.helpers`
- `nilearn._utils.versions`
- `nilearn.glm.contrasts`
- `nilearn.glm.first_level`
- `nilearn.glm.first_level.design_matrix`
- `nilearn.glm.first_level.first_level`
- `nilearn.glm.regression`
- `nilearn.glm.thresholding`
- `nilearn.image`
- `nilearn.maskers`
- `nilearn.surface`
- `nilearn.surface.utils`

**Setup Required:**
```python
# Fixtures: shape_4d_default
```

## Step-by-Step Guide

### Step 1: 'Run fit on FLM with different valid masks.'

```python
'Run fit on FLM with different valid masks.'
```

**Verification:**
```python
assert single_run_model.masker_ == masker
```

### Step 2: Assign rk = 3

```python
rk = 3
```

**Verification:**
```python
assert isinstance(single_run_model.mask_img_, Nifti1Image)
```

### Step 3: Assign unknown = generate_fake_fmri_data_and_design(...)

```python
mask, fmri_data, design_matrices = generate_fake_fmri_data_and_design(shapes=[shape_4d_default], rk=rk)
```

**Verification:**
```python
assert isinstance(z1, Nifti1Image)
```

### Step 4: Assign masker = NiftiMasker(...)

```python
masker = NiftiMasker(mask)
```

### Step 5: Call masker.fit()

```python
masker.fit()
```

### Step 6: Assign single_run_model = FirstLevelModel.fit(...)

```python
single_run_model = FirstLevelModel(mask_img=masker).fit(fmri_data[0], design_matrices=design_matrices[0])
```

**Verification:**
```python
assert single_run_model.masker_ == masker
```

### Step 7: Assign single_run_model = FirstLevelModel.fit(...)

```python
single_run_model = FirstLevelModel(mask_img=None).fit(fmri_data[0], design_matrices=design_matrices[0])
```

**Verification:**
```python
assert isinstance(single_run_model.mask_img_, Nifti1Image)
```

### Step 8: Assign single_run_model = FirstLevelModel.fit(...)

```python
single_run_model = FirstLevelModel(mask_img=mask).fit(fmri_data[0], design_matrices=design_matrices[0])
```

### Step 9: Assign z1 = single_run_model.compute_contrast(...)

```python
z1 = single_run_model.compute_contrast(np.eye(rk)[:1])
```

**Verification:**
```python
assert isinstance(z1, Nifti1Image)
```


## Complete Example

```python
# Setup
# Fixtures: shape_4d_default

# Workflow
'Run fit on FLM with different valid masks.'
rk = 3
mask, fmri_data, design_matrices = generate_fake_fmri_data_and_design(shapes=[shape_4d_default], rk=rk)
masker = NiftiMasker(mask)
masker.fit()
single_run_model = FirstLevelModel(mask_img=masker).fit(fmri_data[0], design_matrices=design_matrices[0])
assert single_run_model.masker_ == masker
single_run_model = FirstLevelModel(mask_img=None).fit(fmri_data[0], design_matrices=design_matrices[0])
assert isinstance(single_run_model.mask_img_, Nifti1Image)
single_run_model = FirstLevelModel(mask_img=mask).fit(fmri_data[0], design_matrices=design_matrices[0])
z1 = single_run_model.compute_contrast(np.eye(rk)[:1])
assert isinstance(z1, Nifti1Image)
```

## Next Steps


---

*Source: test_first_level.py:140 | Complexity: Advanced | Last updated: 2026-05-18*