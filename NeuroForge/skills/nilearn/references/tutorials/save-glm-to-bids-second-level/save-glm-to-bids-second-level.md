# How To: Save Glm To Bids Second Level

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test save_glm_to_bids on a SecondLevelModel.

This test reuses code from
nilearn.glm.tests.test_second_level.test_high_level_glm_with_paths.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `json`
- `warnings`
- `numpy`
- `pandas`
- `pytest`
- `nilearn._utils.data_gen`
- `nilearn._utils.helpers`
- `nilearn.glm.first_level`
- `nilearn.glm.io`
- `nilearn.glm.second_level`
- `nilearn.maskers`

**Setup Required:**
```python
# Fixtures: tmp_path_factory, prefix
```

## Step-by-Step Guide

### Step 1: 'Test save_glm_to_bids on a SecondLevelModel.\n\n    This test reuses code from\n    nilearn.glm.tests.test_second_level.test_high_level_glm_with_paths.\n    '

```python
'Test save_glm_to_bids on a SecondLevelModel.\n\n    This test reuses code from\n    nilearn.glm.tests.test_second_level.test_high_level_glm_with_paths.\n    '
```

**Verification:**
```python
assert (tmpdir / 'dataset_description.json').exists()
```

### Step 2: Assign tmpdir = tmp_path_factory.mktemp(...)

```python
tmpdir = tmp_path_factory.mktemp('test_save_glm_to_bids_second_level')
```

**Verification:**
```python
assert (tmpdir / 'group' / f'{prefix}_{fname}').exists()
```

### Step 3: Assign EXPECTED_FILENAMES = value

```python
EXPECTED_FILENAMES = ['contrast-effectsOfInterest_stat-F_statmap.nii.gz', 'contrast-effectsOfInterest_stat-effect_statmap.nii.gz', 'contrast-effectsOfInterest_stat-p_statmap.nii.gz', 'contrast-effectsOfInterest_stat-variance_statmap.nii.gz', 'contrast-effectsOfInterest_stat-z_statmap.nii.gz', 'contrast-effectsOfInterest_clusters.tsv', 'contrast-effectsOfInterest_clusters.json', 'design.tsv', 'stat-errorts_statmap.nii.gz', 'stat-rsquared_statmap.nii.gz', 'statmap.json', 'mask.nii.gz', 'report.html']
```

### Step 4: Assign shapes = value

```python
shapes = ((3, 3, 3, 1),)
```

### Step 5: Assign rk = 3

```python
rk = 3
```

### Step 6: Assign unknown = generate_fake_fmri_data_and_design(...)

```python
mask, fmri_data, _ = generate_fake_fmri_data_and_design(shapes, rk)
```

### Step 7: Assign fmri_data = value

```python
fmri_data = fmri_data[0]
```

### Step 8: Assign model = SecondLevelModel(...)

```python
model = SecondLevelModel(mask_img=mask, minimize_memory=False)
```

### Step 9: Assign Y = value

```python
Y = [fmri_data] * 2
```

### Step 10: Assign X = pd.DataFrame(...)

```python
X = pd.DataFrame([[1]] * 2, columns=['intercept'])
```

### Step 11: Assign model = model.fit(...)

```python
model = model.fit(Y, design_matrix=X)
```

### Step 12: Assign contrasts = value

```python
contrasts = {'effects of interest': np.eye(len(model.design_matrix_.columns))[0]}
```

### Step 13: Assign contrast_types = value

```python
contrast_types = {'effects of interest': 'F'}
```

### Step 14: Call save_glm_to_bids()

```python
save_glm_to_bids(model=model, contrasts=contrasts, contrast_types=contrast_types, out_dir=tmpdir, prefix=prefix, **KWARGS)
```

**Verification:**
```python
assert (tmpdir / 'dataset_description.json').exists()
```

### Step 15: Call EXPECTED_FILENAMES.extend()

```python
EXPECTED_FILENAMES.extend(['design.png', 'contrast-effectsOfInterest_design.png'])
```

**Verification:**
```python
assert (tmpdir / 'group' / f'{prefix}_{fname}').exists()
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path_factory, prefix

# Workflow
'Test save_glm_to_bids on a SecondLevelModel.\n\n    This test reuses code from\n    nilearn.glm.tests.test_second_level.test_high_level_glm_with_paths.\n    '
tmpdir = tmp_path_factory.mktemp('test_save_glm_to_bids_second_level')
EXPECTED_FILENAMES = ['contrast-effectsOfInterest_stat-F_statmap.nii.gz', 'contrast-effectsOfInterest_stat-effect_statmap.nii.gz', 'contrast-effectsOfInterest_stat-p_statmap.nii.gz', 'contrast-effectsOfInterest_stat-variance_statmap.nii.gz', 'contrast-effectsOfInterest_stat-z_statmap.nii.gz', 'contrast-effectsOfInterest_clusters.tsv', 'contrast-effectsOfInterest_clusters.json', 'design.tsv', 'stat-errorts_statmap.nii.gz', 'stat-rsquared_statmap.nii.gz', 'statmap.json', 'mask.nii.gz', 'report.html']
if is_matplotlib_installed():
    EXPECTED_FILENAMES.extend(['design.png', 'contrast-effectsOfInterest_design.png'])
shapes = ((3, 3, 3, 1),)
rk = 3
mask, fmri_data, _ = generate_fake_fmri_data_and_design(shapes, rk)
fmri_data = fmri_data[0]
model = SecondLevelModel(mask_img=mask, minimize_memory=False)
Y = [fmri_data] * 2
X = pd.DataFrame([[1]] * 2, columns=['intercept'])
model = model.fit(Y, design_matrix=X)
contrasts = {'effects of interest': np.eye(len(model.design_matrix_.columns))[0]}
contrast_types = {'effects of interest': 'F'}
save_glm_to_bids(model=model, contrasts=contrasts, contrast_types=contrast_types, out_dir=tmpdir, prefix=prefix, **KWARGS)
assert (tmpdir / 'dataset_description.json').exists()
for fname in EXPECTED_FILENAMES:
    assert (tmpdir / 'group' / f'{prefix}_{fname}').exists()
```

## Next Steps


---

*Source: test_io.py:327 | Complexity: Advanced | Last updated: 2026-05-18*