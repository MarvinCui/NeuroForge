# How To: With Flm Objects

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: See https://github.com/nilearn/nilearn/issues/3579 .

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
# Fixtures: shape_3d_default
```

## Step-by-Step Guide

### Step 1: 'See https://github.com/nilearn/nilearn/issues/3579 .'

```python
'See https://github.com/nilearn/nilearn/issues/3579 .'
```

### Step 2: Assign unknown = generate_fake_fmri_data_and_design(...)

```python
mask, fmri_data, design_matrices = generate_fake_fmri_data_and_design(shapes=[(*shape_3d_default, 15)])
```

### Step 3: Assign masker = NiftiMasker(...)

```python
masker = NiftiMasker(mask)
```

### Step 4: Call masker.fit()

```python
masker.fit()
```

### Step 5: Assign single_run_model = FirstLevelModel.fit(...)

```python
single_run_model = FirstLevelModel(mask_img=masker).fit(fmri_data[0], design_matrices=design_matrices[0])
```

### Step 6: Call single_run_model.compute_contrast()

```python
single_run_model.compute_contrast('x')
```

### Step 7: Assign second_level_input = value

```python
second_level_input = [single_run_model, single_run_model]
```

### Step 8: Assign design_matrix = pd.DataFrame(...)

```python
design_matrix = pd.DataFrame([1] * len(second_level_input), columns=['intercept'])
```

### Step 9: Call non_parametric_inference()

```python
non_parametric_inference(second_level_input=second_level_input, design_matrix=design_matrix, first_level_contrast='x', n_perm=N_PERM)
```


## Complete Example

```python
# Setup
# Fixtures: shape_3d_default

# Workflow
'See https://github.com/nilearn/nilearn/issues/3579 .'
mask, fmri_data, design_matrices = generate_fake_fmri_data_and_design(shapes=[(*shape_3d_default, 15)])
masker = NiftiMasker(mask)
masker.fit()
single_run_model = FirstLevelModel(mask_img=masker).fit(fmri_data[0], design_matrices=design_matrices[0])
single_run_model.compute_contrast('x')
second_level_input = [single_run_model, single_run_model]
design_matrix = pd.DataFrame([1] * len(second_level_input), columns=['intercept'])
non_parametric_inference(second_level_input=second_level_input, design_matrix=design_matrix, first_level_contrast='x', n_perm=N_PERM)
```

## Next Steps


---

*Source: test_non_parametric_inference.py:29 | Complexity: Advanced | Last updated: 2026-05-18*