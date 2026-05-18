# How To: Tfce

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test non-parametric inference with TFCE inference.

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

### Step 1: 'Test non-parametric inference with TFCE inference.'

```python
'Test non-parametric inference with TFCE inference.'
```

**Verification:**
```python
assert isinstance(out, dict)
```

### Step 2: Assign shapes = value

```python
shapes = [SHAPE] * n_subjects
```

**Verification:**
```python
assert 't' in out
```

### Step 3: Assign unknown = generate_fake_fmri_data_and_design(...)

```python
mask, fmri_data, _ = generate_fake_fmri_data_and_design(shapes)
```

**Verification:**
```python
assert 'tfce' in out
```

### Step 4: Assign X = pd.DataFrame(...)

```python
X = pd.DataFrame([[1]] * n_subjects, columns=['intercept'])
```

**Verification:**
```python
assert 'logp_max_t' in out
```

### Step 5: Assign out = non_parametric_inference(...)

```python
out = non_parametric_inference(fmri_data, design_matrix=X, model_intercept=False, mask=mask, n_perm=N_PERM, tfce=True)
```

**Verification:**
```python
assert 'logp_max_tfce' in out
```


## Complete Example

```python
# Setup
# Fixtures: n_subjects

# Workflow
'Test non-parametric inference with TFCE inference.'
shapes = [SHAPE] * n_subjects
mask, fmri_data, _ = generate_fake_fmri_data_and_design(shapes)
X = pd.DataFrame([[1]] * n_subjects, columns=['intercept'])
out = non_parametric_inference(fmri_data, design_matrix=X, model_intercept=False, mask=mask, n_perm=N_PERM, tfce=True)
assert isinstance(out, dict)
assert 't' in out
assert 'tfce' in out
assert 'logp_max_t' in out
assert 'logp_max_tfce' in out
assert get_data(out['tfce']).shape == shapes[0][:3]
assert get_data(out['logp_max_tfce']).shape == shapes[0][:3]
```

## Next Steps


---

*Source: test_non_parametric_inference.py:198 | Complexity: Intermediate | Last updated: 2026-05-18*