# How To: Permutation Computation

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test non_parametric_inference.

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

### Step 1: 'Test non_parametric_inference.'

```python
'Test non_parametric_inference.'
```

**Verification:**
```python
assert get_data(neg_log_pvals_img).shape == SHAPE[:3]
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

### Step 5: Assign neg_log_pvals_img = non_parametric_inference(...)

```python
neg_log_pvals_img = non_parametric_inference(Y, design_matrix=X, model_intercept=False, mask=mask, n_perm=N_PERM)
```

**Verification:**
```python
assert get_data(neg_log_pvals_img).shape == SHAPE[:3]
```


## Complete Example

```python
# Setup
# Fixtures: n_subjects

# Workflow
'Test non_parametric_inference.'
func_img, mask = fake_fmri_data()
Y = [func_img] * n_subjects
X = pd.DataFrame([[1]] * n_subjects, columns=['intercept'])
neg_log_pvals_img = non_parametric_inference(Y, design_matrix=X, model_intercept=False, mask=mask, n_perm=N_PERM)
assert get_data(neg_log_pvals_img).shape == SHAPE[:3]
```

## Next Steps


---

*Source: test_non_parametric_inference.py:183 | Complexity: Intermediate | Last updated: 2026-05-18*