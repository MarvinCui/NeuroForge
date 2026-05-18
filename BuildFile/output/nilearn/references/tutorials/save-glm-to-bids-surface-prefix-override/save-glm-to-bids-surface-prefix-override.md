# How To: Save Glm To Bids Surface Prefix Override

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Save surface GLM results to disk with prefix.

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
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Save surface GLM results to disk with prefix.'

```python
'Save surface GLM results to disk with prefix.'
```

**Verification:**
```python
assert (tmp_path / 'output' / sub_prefix / f'{prefix}{fname}').exists()
```

### Step 2: Assign n_sub = 1

```python
n_sub = 1
```

### Step 3: Assign bids_path = create_fake_bids_dataset(...)

```python
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=n_sub, n_ses=2, tasks=['main'], n_runs=[2], n_vertices=10242)
```

### Step 4: Assign unknown = first_level_from_bids(...)

```python
models, imgs, events, _ = first_level_from_bids(dataset_path=bids_path, task_label='main', space_label='fsaverage5', slice_time_ref=0.0)
```

### Step 5: Assign model = value

```python
model = models[0]
```

### Step 6: Assign run_imgs = value

```python
run_imgs = imgs[0]
```

### Step 7: Assign events = value

```python
events = events[0]
```

### Step 8: Assign model.minimize_memory = False

```python
model.minimize_memory = False
```

### Step 9: Call model.fit()

```python
model.fit(run_imgs=run_imgs, events=events)
```

### Step 10: Assign prefix = 'sub-01'

```python
prefix = 'sub-01'
```

### Step 11: Assign model = save_glm_to_bids(...)

```python
model = save_glm_to_bids(model=model, out_dir=tmp_path / 'output', contrasts=['c0'], prefix=prefix, **KWARGS)
```

### Step 12: Assign EXPECTED_FILENAME_ENDINGS = value

```python
EXPECTED_FILENAME_ENDINGS = ['run-2_design.tsv', 'run-2_design.json', 'hemi-L_den-10242_mask.gii', 'hemi-R_den-10242_mask.gii', 'hemi-L_den-10242_contrast-c0_stat-z_statmap.gii', 'hemi-R_den-10242_contrast-c0_stat-z_statmap.gii', 'run-1_hemi-L_den-10242_stat-rsquared_statmap.gii', 'run-1_hemi-R_den-10242_stat-rsquared_statmap.gii', 'contrast-c0_clusters.tsv', 'contrast-c0_clusters.json']
```

### Step 13: Assign sub_prefix = value

```python
sub_prefix = prefix.split('_')[0] if prefix.startswith('sub-') else ''
```

### Step 14: Call EXPECTED_FILENAME_ENDINGS.extend()

```python
EXPECTED_FILENAME_ENDINGS.extend(['run-1_design.png', 'run-1_corrdesign.png', 'run-2_contrast-c0_design.png'])
```

**Verification:**
```python
assert (tmp_path / 'output' / sub_prefix / f'{prefix}{fname}').exists()
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Save surface GLM results to disk with prefix.'
n_sub = 1
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=n_sub, n_ses=2, tasks=['main'], n_runs=[2], n_vertices=10242)
models, imgs, events, _ = first_level_from_bids(dataset_path=bids_path, task_label='main', space_label='fsaverage5', slice_time_ref=0.0)
model = models[0]
run_imgs = imgs[0]
events = events[0]
model.minimize_memory = False
model.fit(run_imgs=run_imgs, events=events)
prefix = 'sub-01'
model = save_glm_to_bids(model=model, out_dir=tmp_path / 'output', contrasts=['c0'], prefix=prefix, **KWARGS)
EXPECTED_FILENAME_ENDINGS = ['run-2_design.tsv', 'run-2_design.json', 'hemi-L_den-10242_mask.gii', 'hemi-R_den-10242_mask.gii', 'hemi-L_den-10242_contrast-c0_stat-z_statmap.gii', 'hemi-R_den-10242_contrast-c0_stat-z_statmap.gii', 'run-1_hemi-L_den-10242_stat-rsquared_statmap.gii', 'run-1_hemi-R_den-10242_stat-rsquared_statmap.gii', 'contrast-c0_clusters.tsv', 'contrast-c0_clusters.json']
if is_matplotlib_installed():
    EXPECTED_FILENAME_ENDINGS.extend(['run-1_design.png', 'run-1_corrdesign.png', 'run-2_contrast-c0_design.png'])
if prefix != '' and (not prefix.endswith('_')):
    prefix += '_'
sub_prefix = prefix.split('_')[0] if prefix.startswith('sub-') else ''
for fname in EXPECTED_FILENAME_ENDINGS:
    assert (tmp_path / 'output' / sub_prefix / f'{prefix}{fname}').exists()
```

## Next Steps


---

*Source: test_io.py:588 | Complexity: Advanced | Last updated: 2026-05-18*