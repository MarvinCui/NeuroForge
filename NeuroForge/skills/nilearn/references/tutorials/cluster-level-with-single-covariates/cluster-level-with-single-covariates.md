# How To: Cluster Level With Single Covariates

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test non-parametric inference with cluster-level inference in     the context of covariates.
    

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
# Fixtures: shape_3d_default, rng, n_subjects
```

## Step-by-Step Guide

### Step 1: 'Test non-parametric inference with cluster-level inference in     the context of covariates.\n    '

```python
'Test non-parametric inference with cluster-level inference in     the context of covariates.\n    '
```

### Step 2: Assign shapes = value

```python
shapes = ((*shape_3d_default, 1),)
```

### Step 3: Assign unknown = generate_fake_fmri_data_and_design(...)

```python
mask, fmri_data, _ = generate_fake_fmri_data_and_design(shapes)
```

### Step 4: Assign unc_pval = 0.1

```python
unc_pval = 0.1
```

### Step 5: Assign kernels = rng.uniform(...)

```python
kernels = rng.uniform(low=0, high=5, size=n_subjects)
```

### Step 6: Assign Y = value

```python
Y = [smooth_img(fmri_data[0], kernel) for kernel in kernels]
```

### Step 7: Assign X = pd.DataFrame(...)

```python
X = pd.DataFrame({'intercept': [1] * len(Y)})
```

### Step 8: Call non_parametric_inference()

```python
non_parametric_inference(Y, design_matrix=X, mask=mask, model_intercept=False, second_level_contrast='intercept', n_perm=N_PERM, threshold=unc_pval)
```


## Complete Example

```python
# Setup
# Fixtures: shape_3d_default, rng, n_subjects

# Workflow
'Test non-parametric inference with cluster-level inference in     the context of covariates.\n    '
shapes = ((*shape_3d_default, 1),)
mask, fmri_data, _ = generate_fake_fmri_data_and_design(shapes)
unc_pval = 0.1
kernels = rng.uniform(low=0, high=5, size=n_subjects)
Y = [smooth_img(fmri_data[0], kernel) for kernel in kernels]
X = pd.DataFrame({'intercept': [1] * len(Y)})
non_parametric_inference(Y, design_matrix=X, mask=mask, model_intercept=False, second_level_contrast='intercept', n_perm=N_PERM, threshold=unc_pval)
```

## Next Steps


---

*Source: test_non_parametric_inference.py:301 | Complexity: Advanced | Last updated: 2026-05-18*