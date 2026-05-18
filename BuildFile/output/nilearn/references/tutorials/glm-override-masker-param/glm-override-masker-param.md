# How To: Glm Override Masker Param

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check masker parameters overridden by the FirstLevelModel parameters.

Give a fitted NiftiMasker with a None mask_img_ attribute
and check that the masker parameters are overridden by the
FirstLevelModel parameters.

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

### Step 1: 'Check masker parameters overridden by the FirstLevelModel parameters.\n\n    Give a fitted NiftiMasker with a None mask_img_ attribute\n    and check that the masker parameters are overridden by the\n    FirstLevelModel parameters.\n    '

```python
'Check masker parameters overridden by the FirstLevelModel parameters.\n\n    Give a fitted NiftiMasker with a None mask_img_ attribute\n    and check that the masker parameters are overridden by the\n    FirstLevelModel parameters.\n    '
```

### Step 2: Assign rk = 3

```python
rk = 3
```

### Step 3: Assign unknown = generate_fake_fmri_data_and_design(...)

```python
mask, fmri_data, design_matrices = generate_fake_fmri_data_and_design(shapes=[shape_4d_default], rk=rk)
```

### Step 4: Assign masker = NiftiMasker(...)

```python
masker = NiftiMasker(mask)
```

### Step 5: Call masker.fit()

```python
masker.fit()
```

### Step 6: Assign masker.mask_img_ = None

```python
masker.mask_img_ = None
```

### Step 7: Call FirstLevelModel.fit()

```python
FirstLevelModel(mask_img=masker).fit(fmri_data[0], design_matrices=design_matrices[0])
```


## Complete Example

```python
# Setup
# Fixtures: shape_4d_default

# Workflow
'Check masker parameters overridden by the FirstLevelModel parameters.\n\n    Give a fitted NiftiMasker with a None mask_img_ attribute\n    and check that the masker parameters are overridden by the\n    FirstLevelModel parameters.\n    '
rk = 3
mask, fmri_data, design_matrices = generate_fake_fmri_data_and_design(shapes=[shape_4d_default], rk=rk)
masker = NiftiMasker(mask)
masker.fit()
masker.mask_img_ = None
with pytest.warns(UserWarning, match='Overriding provided-default estimator parameters with provided masker parameters'):
    FirstLevelModel(mask_img=masker).fit(fmri_data[0], design_matrices=design_matrices[0])
```

## Next Steps


---

*Source: test_first_level.py:113 | Complexity: Intermediate | Last updated: 2026-05-18*