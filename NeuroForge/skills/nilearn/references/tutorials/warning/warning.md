# How To: Warning

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test warning smoothing_fwhm override.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pandas`
- `pytest`
- `nibabel`
- `numpy.testing`
- `scipy`
- `nilearn._utils.data_gen`
- `nilearn.exceptions`
- `nilearn.glm.first_level`
- `nilearn.glm.second_level`
- `nilearn.image`
- `nilearn.maskers`
- `nilearn.reporting`
- `conftest`

**Setup Required:**
```python
# Fixtures: n_subjects
```

## Step-by-Step Guide

### Step 1: 'Test warning smoothing_fwhm override.'

```python
'Test warning smoothing_fwhm override.'
```

### Step 2: Assign unknown = fake_fmri_data(...)

```python
func_img, mask = fake_fmri_data()
```

### Step 3: Assign Y = value

```python
Y = [func_img] * n_subjects
```

### Step 4: Assign X = pd.DataFrame(...)

```python
X = pd.DataFrame([[1]] * n_subjects, columns=['intercept'])
```

### Step 5: Assign c1 = value

```python
c1 = np.eye(len(X.columns))[0]
```

### Step 6: Assign masker = NiftiMasker(...)

```python
masker = NiftiMasker(mask, smoothing_fwhm=2.0, standardize=None)
```

### Step 7: Call non_parametric_inference()

```python
non_parametric_inference(Y, design_matrix=X, second_level_contrast=c1, smoothing_fwhm=3.0, mask=masker, n_perm=N_PERM)
```


## Complete Example

```python
# Setup
# Fixtures: n_subjects

# Workflow
'Test warning smoothing_fwhm override.'
func_img, mask = fake_fmri_data()
Y = [func_img] * n_subjects
X = pd.DataFrame([[1]] * n_subjects, columns=['intercept'])
c1 = np.eye(len(X.columns))[0]
masker = NiftiMasker(mask, smoothing_fwhm=2.0, standardize=None)
with pytest.warns(UserWarning, match="Parameter 'smoothing_fwhm' of the masker overridden"):
    non_parametric_inference(Y, design_matrix=X, second_level_contrast=c1, smoothing_fwhm=3.0, mask=masker, n_perm=N_PERM)
```

## Next Steps


---

*Source: test_non_parametric_inference.py:97 | Complexity: Intermediate | Last updated: 2026-05-18*