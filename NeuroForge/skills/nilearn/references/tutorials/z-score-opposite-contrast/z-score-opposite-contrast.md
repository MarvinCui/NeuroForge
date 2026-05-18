# How To: Z Score Opposite Contrast

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test z score opposite contrast

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `scipy.linalg`
- `scipy.stats`
- `numpy.testing`
- `scipy.stats`
- `nilearn._utils.data_gen`
- `nilearn.glm._utils`
- `nilearn.glm.first_level`
- `nilearn.maskers`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign unknown = generate_fake_fmri(...)

```python
fmri, mask = generate_fake_fmri(shape=(50, 20, 50), length=96, random_state=rng)
```

**Verification:**
```python
assert_almost_equal(z_map_seed1_vs_seed2.get_fdata(dtype='float32').min(), -z_map_seed2_vs_seed1.get_fdata(dtype='float32').max(), decimal=10)
```

### Step 2: Assign nifti_masker = NiftiMasker(...)

```python
nifti_masker = NiftiMasker(mask_img=mask, standardize=None)
```

**Verification:**
```python
assert_almost_equal(z_map_seed1_vs_seed2.get_fdata(dtype='float32').max(), -z_map_seed2_vs_seed1.get_fdata(dtype='float32').min(), decimal=10)
```

### Step 3: Assign data = nifti_masker.fit_transform(...)

```python
data = nifti_masker.fit_transform(fmri)
```

### Step 4: Assign frametimes = np.linspace(...)

```python
frametimes = np.linspace(0, (96 - 1) * 2, 96)
```

### Step 5: Assign design_matrix = make_first_level_design_matrix(...)

```python
design_matrix = make_first_level_design_matrix(frametimes, hrf_model='spm', add_regs=np.array(data[:, i]).reshape(-1, 1))
```

### Step 6: Assign c1 = np.array(...)

```python
c1 = np.array([1] + [0] * (design_matrix.shape[1] - 1))
```

### Step 7: Assign c2 = np.array(...)

```python
c2 = np.array([0] + [1] + [0] * (design_matrix.shape[1] - 2))
```

### Step 8: Assign contrasts = value

```python
contrasts = {'seed1 - seed2': c1 - c2, 'seed2 - seed1': c2 - c1}
```

### Step 9: Assign fmri_glm = FirstLevelModel(...)

```python
fmri_glm = FirstLevelModel(t_r=2.0, noise_model='ar1', standardize=False, hrf_model='spm', drift_model='cosine')
```

### Step 10: Call fmri_glm.fit()

```python
fmri_glm.fit(fmri, design_matrices=design_matrix)
```

### Step 11: Assign z_map_seed1_vs_seed2 = fmri_glm.compute_contrast(...)

```python
z_map_seed1_vs_seed2 = fmri_glm.compute_contrast(contrasts['seed1 - seed2'], output_type='z_score')
```

### Step 12: Assign z_map_seed2_vs_seed1 = fmri_glm.compute_contrast(...)

```python
z_map_seed2_vs_seed1 = fmri_glm.compute_contrast(contrasts['seed2 - seed1'], output_type='z_score')
```

### Step 13: Call assert_almost_equal()

```python
assert_almost_equal(z_map_seed1_vs_seed2.get_fdata(dtype='float32').min(), -z_map_seed2_vs_seed1.get_fdata(dtype='float32').max(), decimal=10)
```

### Step 14: Call assert_almost_equal()

```python
assert_almost_equal(z_map_seed1_vs_seed2.get_fdata(dtype='float32').max(), -z_map_seed2_vs_seed1.get_fdata(dtype='float32').min(), decimal=10)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
fmri, mask = generate_fake_fmri(shape=(50, 20, 50), length=96, random_state=rng)
nifti_masker = NiftiMasker(mask_img=mask, standardize=None)
data = nifti_masker.fit_transform(fmri)
frametimes = np.linspace(0, (96 - 1) * 2, 96)
for i in [0, 20]:
    design_matrix = make_first_level_design_matrix(frametimes, hrf_model='spm', add_regs=np.array(data[:, i]).reshape(-1, 1))
    c1 = np.array([1] + [0] * (design_matrix.shape[1] - 1))
    c2 = np.array([0] + [1] + [0] * (design_matrix.shape[1] - 2))
    contrasts = {'seed1 - seed2': c1 - c2, 'seed2 - seed1': c2 - c1}
    fmri_glm = FirstLevelModel(t_r=2.0, noise_model='ar1', standardize=False, hrf_model='spm', drift_model='cosine')
    fmri_glm.fit(fmri, design_matrices=design_matrix)
    z_map_seed1_vs_seed2 = fmri_glm.compute_contrast(contrasts['seed1 - seed2'], output_type='z_score')
    z_map_seed2_vs_seed1 = fmri_glm.compute_contrast(contrasts['seed2 - seed1'], output_type='z_score')
    assert_almost_equal(z_map_seed1_vs_seed2.get_fdata(dtype='float32').min(), -z_map_seed2_vs_seed1.get_fdata(dtype='float32').max(), decimal=10)
    assert_almost_equal(z_map_seed1_vs_seed2.get_fdata(dtype='float32').max(), -z_map_seed2_vs_seed1.get_fdata(dtype='float32').min(), decimal=10)
```

## Next Steps


---

*Source: test_utils.py:118 | Complexity: Advanced | Last updated: 2026-05-18*