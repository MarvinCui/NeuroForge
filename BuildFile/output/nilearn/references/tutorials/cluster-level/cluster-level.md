# How To: Cluster Level

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test non-parametric inference with cluster-level inference.

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

### Step 1: 'Test non-parametric inference with cluster-level inference.'

```python
'Test non-parametric inference with cluster-level inference.'
```

**Verification:**
```python
assert isinstance(out, dict)
```

### Step 2: Assign unknown = fake_fmri_data(...)

```python
func_img, mask = fake_fmri_data()
```

**Verification:**
```python
assert 't' in out
```

### Step 3: Assign Y = value

```python
Y = [func_img] * n_subjects
```

**Verification:**
```python
assert 'logp_max_t' in out
```

### Step 4: Assign X = pd.DataFrame(...)

```python
X = pd.DataFrame([[1]] * n_subjects, columns=['intercept'])
```

**Verification:**
```python
assert 'size' in out
```

### Step 5: Assign out = non_parametric_inference(...)

```python
out = non_parametric_inference(Y, design_matrix=X, model_intercept=False, mask=mask, n_perm=N_PERM, threshold=0.001)
```

**Verification:**
```python
assert 'logp_max_size' in out
```


## Complete Example

```python
# Setup
# Fixtures: n_subjects

# Workflow
'Test non-parametric inference with cluster-level inference.'
func_img, mask = fake_fmri_data()
Y = [func_img] * n_subjects
X = pd.DataFrame([[1]] * n_subjects, columns=['intercept'])
out = non_parametric_inference(Y, design_matrix=X, model_intercept=False, mask=mask, n_perm=N_PERM, threshold=0.001)
assert isinstance(out, dict)
assert 't' in out
assert 'logp_max_t' in out
assert 'size' in out
assert 'logp_max_size' in out
assert 'mass' in out
assert 'logp_max_mass' in out
assert get_data(out['logp_max_t']).shape == SHAPE[:3]
```

## Next Steps


---

*Source: test_non_parametric_inference.py:223 | Complexity: Intermediate | Last updated: 2026-05-18*