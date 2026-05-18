# How To: Save Glm To Bids Contrast Definitions

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test that save_glm_to_bids operates on different contrast definitions        as expected.

- Test string-based contrasts and undefined contrast types

This test reuses code from
nilearn.glm.tests.test_first_level.test_high_level_glm_one_session.

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
# Fixtures: tmp_path_factory, two_runs_model, contrasts, prefix
```

## Step-by-Step Guide

### Step 1: 'Test that save_glm_to_bids operates on different contrast definitions        as expected.\n\n    - Test string-based contrasts and undefined contrast types\n\n    This test reuses code from\n    nilearn.glm.tests.test_first_level.test_high_level_glm_one_session.\n    '

```python
'Test that save_glm_to_bids operates on different contrast definitions        as expected.\n\n    - Test string-based contrasts and undefined contrast types\n\n    This test reuses code from\n    nilearn.glm.tests.test_first_level.test_high_level_glm_one_session.\n    '
```

**Verification:**
```python
assert (tmpdir / 'dataset_description.json').exists()
```

### Step 2: Assign tmpdir = tmp_path_factory.mktemp(...)

```python
tmpdir = tmp_path_factory.mktemp('test_save_glm_to_bids_contrast_definitions')
```

**Verification:**
```python
assert (tmpdir / sub_prefix / f'{prefix}{fname}').exists()
```

### Step 3: Assign EXPECTED_FILENAME_ENDINGS = value

```python
EXPECTED_FILENAME_ENDINGS = ['contrast-aaaMinusBbb_stat-effect_statmap.nii.gz', 'contrast-aaaMinusBbb_stat-p_statmap.nii.gz', 'contrast-aaaMinusBbb_stat-t_statmap.nii.gz', 'contrast-aaaMinusBbb_stat-variance_statmap.nii.gz', 'contrast-aaaMinusBbb_stat-z_statmap.nii.gz', 'contrast-aaaMinusBbb_clusters.tsv', 'contrast-aaaMinusBbb_clusters.json', 'run-1_design.tsv', 'run-1_design.json', 'run-1_stat-errorts_statmap.nii.gz', 'run-1_stat-rsquared_statmap.nii.gz', 'run-2_design.tsv', 'run-2_design.json', 'run-2_stat-errorts_statmap.nii.gz', 'run-2_stat-rsquared_statmap.nii.gz', 'statmap.json', 'mask.nii.gz', 'report.html']
```

### Step 4: Call save_glm_to_bids()

```python
save_glm_to_bids(model=two_runs_model, contrasts=contrasts, contrast_types=None, out_dir=tmpdir, prefix=prefix, **KWARGS)
```

**Verification:**
```python
assert (tmpdir / 'dataset_description.json').exists()
```

### Step 5: Assign sub_prefix = value

```python
sub_prefix = prefix.split('_')[0] if prefix.startswith('sub-') else ''
```

### Step 6: Call EXPECTED_FILENAME_ENDINGS.extend()

```python
EXPECTED_FILENAME_ENDINGS.extend(['run-1_contrast-aaaMinusBbb_design.png', 'run-1_design.png', 'run-2_contrast-aaaMinusBbb_design.png', 'run-2_design.png'])
```

### Step 7: Assign prefix = ''

```python
prefix = ''
```

### Step 8: Assign prefix = value

```python
prefix = f'{prefix}_'
```

**Verification:**
```python
assert (tmpdir / sub_prefix / f'{prefix}{fname}').exists()
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path_factory, two_runs_model, contrasts, prefix

# Workflow
'Test that save_glm_to_bids operates on different contrast definitions        as expected.\n\n    - Test string-based contrasts and undefined contrast types\n\n    This test reuses code from\n    nilearn.glm.tests.test_first_level.test_high_level_glm_one_session.\n    '
tmpdir = tmp_path_factory.mktemp('test_save_glm_to_bids_contrast_definitions')
EXPECTED_FILENAME_ENDINGS = ['contrast-aaaMinusBbb_stat-effect_statmap.nii.gz', 'contrast-aaaMinusBbb_stat-p_statmap.nii.gz', 'contrast-aaaMinusBbb_stat-t_statmap.nii.gz', 'contrast-aaaMinusBbb_stat-variance_statmap.nii.gz', 'contrast-aaaMinusBbb_stat-z_statmap.nii.gz', 'contrast-aaaMinusBbb_clusters.tsv', 'contrast-aaaMinusBbb_clusters.json', 'run-1_design.tsv', 'run-1_design.json', 'run-1_stat-errorts_statmap.nii.gz', 'run-1_stat-rsquared_statmap.nii.gz', 'run-2_design.tsv', 'run-2_design.json', 'run-2_stat-errorts_statmap.nii.gz', 'run-2_stat-rsquared_statmap.nii.gz', 'statmap.json', 'mask.nii.gz', 'report.html']
if is_matplotlib_installed():
    EXPECTED_FILENAME_ENDINGS.extend(['run-1_contrast-aaaMinusBbb_design.png', 'run-1_design.png', 'run-2_contrast-aaaMinusBbb_design.png', 'run-2_design.png'])
save_glm_to_bids(model=two_runs_model, contrasts=contrasts, contrast_types=None, out_dir=tmpdir, prefix=prefix, **KWARGS)
assert (tmpdir / 'dataset_description.json').exists()
if not isinstance(prefix, str):
    prefix = ''
if prefix and (not prefix.endswith('_')):
    prefix = f'{prefix}_'
sub_prefix = prefix.split('_')[0] if prefix.startswith('sub-') else ''
for fname in EXPECTED_FILENAME_ENDINGS:
    assert (tmpdir / sub_prefix / f'{prefix}{fname}').exists()
```

## Next Steps


---

*Source: test_io.py:256 | Complexity: Advanced | Last updated: 2026-05-18*