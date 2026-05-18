# How To: Mask Img Volume

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check mask_img_ with volume data.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pandas`
- `pytest`
- `nibabel`
- `numpy.testing`
- `sklearn.utils.estimator_checks`
- `nilearn._utils`
- `nilearn._utils.data_gen`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.versions`
- `nilearn.glm.first_level`
- `nilearn.glm.second_level.second_level`
- `nilearn.image`
- `nilearn.maskers`
- `nilearn.surface`
- `nilearn.surface.utils`
- `conftest`

**Setup Required:**
```python
# Fixtures: n_subjects
```

## Step-by-Step Guide

### Step 1: 'Check mask_img_ with volume data.'

```python
'Check mask_img_ with volume data.'
```

**Verification:**
```python
assert isinstance(model.mask_img_, Nifti1Image)
```

### Step 2: Assign unknown = fake_fmri_data(...)

```python
func_img, mask = fake_fmri_data()
```

### Step 3: Assign model = SecondLevelModel(...)

```python
model = SecondLevelModel(mask_img=mask)
```

### Step 4: Assign Y = value

```python
Y = [func_img] * n_subjects
```

### Step 5: Assign X = pd.DataFrame(...)

```python
X = pd.DataFrame([[1]] * n_subjects, columns=['intercept'])
```

### Step 6: Assign model = model.fit(...)

```python
model = model.fit(Y, design_matrix=X)
```

**Verification:**
```python
assert isinstance(model.mask_img_, Nifti1Image)
```


## Complete Example

```python
# Setup
# Fixtures: n_subjects

# Workflow
'Check mask_img_ with volume data.'
func_img, mask = fake_fmri_data()
model = SecondLevelModel(mask_img=mask)
Y = [func_img] * n_subjects
X = pd.DataFrame([[1]] * n_subjects, columns=['intercept'])
model = model.fit(Y, design_matrix=X)
assert isinstance(model.mask_img_, Nifti1Image)
```

## Next Steps


---

*Source: test_second_level.py:463 | Complexity: Intermediate | Last updated: 2026-05-18*