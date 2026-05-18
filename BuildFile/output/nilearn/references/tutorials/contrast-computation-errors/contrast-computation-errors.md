# How To: Contrast Computation Errors

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test invalid contrast values.

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
# Fixtures: rng, n_subjects
```

## Step-by-Step Guide

### Step 1: 'Test invalid contrast values.'

```python
'Test invalid contrast values.'
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

### Step 5: Assign ncol = len(...)

```python
ncol = len(X.columns)
```

### Step 6: Assign unknown = value

```python
_, cnull = (np.eye(ncol)[0, :], np.zeros(ncol))
```

### Step 7: Assign X = pd.DataFrame(...)

```python
X = pd.DataFrame(rng.uniform(size=(n_subjects, 2)), columns=['r1', 'r2'])
```

### Step 8: Call non_parametric_inference()

```python
non_parametric_inference(second_level_input=None, second_level_contrast='intercept', mask=mask)
```

### Step 9: Call non_parametric_inference()

```python
non_parametric_inference(second_level_input=Y, design_matrix=X, second_level_contrast=cnull, mask=mask)
```

### Step 10: Call non_parametric_inference()

```python
non_parametric_inference(second_level_input=Y, design_matrix=X, second_level_contrast=[], mask=mask)
```

### Step 11: Call non_parametric_inference()

```python
non_parametric_inference(second_level_input=Y, design_matrix=X, second_level_contrast=None)
```


## Complete Example

```python
# Setup
# Fixtures: rng, n_subjects

# Workflow
'Test invalid contrast values.'
func_img, mask = fake_fmri_data()
with pytest.raises(TypeError, match='second_level_input must be either'):
    non_parametric_inference(second_level_input=None, second_level_contrast='intercept', mask=mask)
Y = [func_img] * n_subjects
X = pd.DataFrame([[1]] * n_subjects, columns=['intercept'])
ncol = len(X.columns)
_, cnull = (np.eye(ncol)[0, :], np.zeros(ncol))
with pytest.raises(ValueError, match='Second_level_contrast must be a valid'):
    non_parametric_inference(second_level_input=Y, design_matrix=X, second_level_contrast=cnull, mask=mask)
with pytest.raises(ValueError, match='Second_level_contrast must be a valid'):
    non_parametric_inference(second_level_input=Y, design_matrix=X, second_level_contrast=[], mask=mask)
X = pd.DataFrame(rng.uniform(size=(n_subjects, 2)), columns=['r1', 'r2'])
with pytest.raises(ValueError, match='No second-level contrast is specified.'):
    non_parametric_inference(second_level_input=Y, design_matrix=X, second_level_contrast=None)
```

## Next Steps


---

*Source: test_non_parametric_inference.py:368 | Complexity: Advanced | Last updated: 2026-05-18*