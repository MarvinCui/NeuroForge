# How To: With Paths

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Ensure non_parametric_inference can work with paths.

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
# Fixtures: tmp_path, n_subjects
```

## Step-by-Step Guide

### Step 1: 'Ensure non_parametric_inference can work with paths.'

```python
'Ensure non_parametric_inference can work with paths.'
```

**Verification:**
```python
assert all((isinstance(img, Nifti1Image) for img in neg_log_pvals_imgs))
```

### Step 2: Assign unknown = write_fake_fmri_data_and_design(...)

```python
mask_file, fmri_files, _ = write_fake_fmri_data_and_design((SHAPE,), file_path=tmp_path)
```

**Verification:**
```python
assert_array_equal(img.affine, load(mask_file).affine)
```

### Step 3: Assign fmri_files = value

```python
fmri_files = fmri_files[0]
```

**Verification:**
```python
assert np.all(neg_log_pvals <= -np.log10(1.0 / (N_PERM + 1)))
```

### Step 4: Assign df_input = pd.DataFrame(...)

```python
df_input = pd.DataFrame({'subject_label': [f'sub-{i}' for i in range(n_subjects)], 'effects_map_path': [fmri_files] * n_subjects, 'map_name': [fmri_files] * n_subjects})
```

**Verification:**
```python
assert np.all(neg_log_pvals >= 0)
```

### Step 5: Assign func_img = load(...)

```python
func_img = load(fmri_files)
```

### Step 6: Assign Y = value

```python
Y = [func_img] * n_subjects
```

### Step 7: Assign X = pd.DataFrame(...)

```python
X = pd.DataFrame([[1]] * n_subjects, columns=['intercept'])
```

### Step 8: Assign c1 = value

```python
c1 = np.eye(len(X.columns))[0]
```

### Step 9: Assign neg_log_pvals_imgs = value

```python
neg_log_pvals_imgs = [non_parametric_inference(second_level_input, design_matrix=X, second_level_contrast=c1, first_level_contrast=fmri_files, mask=mask_file, n_perm=N_PERM, verbose=1) for second_level_input in [Y, df_input]]
```

**Verification:**
```python
assert all((isinstance(img, Nifti1Image) for img in neg_log_pvals_imgs))
```

### Step 10: Assign neg_log_pvals_list = value

```python
neg_log_pvals_list = [get_data(i) for i in neg_log_pvals_imgs]
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(img.affine, load(mask_file).affine)
```

**Verification:**
```python
assert np.all(neg_log_pvals <= -np.log10(1.0 / (N_PERM + 1)))
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, n_subjects

# Workflow
'Ensure non_parametric_inference can work with paths.'
mask_file, fmri_files, _ = write_fake_fmri_data_and_design((SHAPE,), file_path=tmp_path)
fmri_files = fmri_files[0]
df_input = pd.DataFrame({'subject_label': [f'sub-{i}' for i in range(n_subjects)], 'effects_map_path': [fmri_files] * n_subjects, 'map_name': [fmri_files] * n_subjects})
func_img = load(fmri_files)
Y = [func_img] * n_subjects
X = pd.DataFrame([[1]] * n_subjects, columns=['intercept'])
c1 = np.eye(len(X.columns))[0]
neg_log_pvals_imgs = [non_parametric_inference(second_level_input, design_matrix=X, second_level_contrast=c1, first_level_contrast=fmri_files, mask=mask_file, n_perm=N_PERM, verbose=1) for second_level_input in [Y, df_input]]
assert all((isinstance(img, Nifti1Image) for img in neg_log_pvals_imgs))
for img in neg_log_pvals_imgs:
    assert_array_equal(img.affine, load(mask_file).affine)
neg_log_pvals_list = [get_data(i) for i in neg_log_pvals_imgs]
for neg_log_pvals in neg_log_pvals_list:
    assert np.all(neg_log_pvals <= -np.log10(1.0 / (N_PERM + 1)))
    assert np.all(neg_log_pvals >= 0)
```

## Next Steps


---

*Source: test_non_parametric_inference.py:57 | Complexity: Advanced | Last updated: 2026-05-18*