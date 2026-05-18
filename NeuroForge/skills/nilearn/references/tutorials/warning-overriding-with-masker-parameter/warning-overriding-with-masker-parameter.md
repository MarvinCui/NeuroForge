# How To: Warning Overriding With Masker Parameter

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test warning overriding with masker parameter

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

### Step 1: Assign unknown = fake_fmri_data(...)

```python
func_img, mask = fake_fmri_data()
```

### Step 2: Assign Y = value

```python
Y = [func_img] * n_subjects
```

### Step 3: Assign X = pd.DataFrame(...)

```python
X = pd.DataFrame([[1]] * n_subjects, columns=['intercept'])
```

### Step 4: Assign masker = NiftiMasker.fit(...)

```python
masker = NiftiMasker(mask).fit()
```

### Step 5: Call SecondLevelModel.fit()

```python
SecondLevelModel(mask_img=masker, verbose=1).fit(Y, design_matrix=X)
```


## Complete Example

```python
# Setup
# Fixtures: n_subjects

# Workflow
func_img, mask = fake_fmri_data()
Y = [func_img] * n_subjects
X = pd.DataFrame([[1]] * n_subjects, columns=['intercept'])
masker = NiftiMasker(mask).fit()
with pytest.warns(UserWarning, match='Overriding provided-default estimator parameters with provided masker parameters'):
    SecondLevelModel(mask_img=masker, verbose=1).fit(Y, design_matrix=X)
```

## Next Steps


---

*Source: test_second_level.py:531 | Complexity: Intermediate | Last updated: 2026-05-18*