# How To: Save Glm To Bids Infer Filenames

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check that output filenames can be inferred from BIDS input.

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
# Fixtures: tmp_path, kwargs
```

## Step-by-Step Guide

### Step 1: 'Check that output filenames can be inferred from BIDS input.'

```python
'Check that output filenames can be inferred from BIDS input.'
```

**Verification:**
```python
assert len(model._reporting_data['run_imgs']) == 4
```

### Step 2: Assign n_sub = 1

```python
n_sub = 1
```

**Verification:**
```python
assert (tmp_path / 'output' / 'sub-01' / fname).exists()
```

### Step 3: Assign bids_path = create_fake_bids_dataset(...)

```python
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=n_sub, n_ses=2, tasks=['main'], n_runs=[2], n_voxels=20)
```

**Verification:**
```python
assert key in metadata
```

### Step 4: Assign unknown = first_level_from_bids(...)

```python
models, imgs, events, _ = first_level_from_bids(dataset_path=bids_path, task_label='main', space_label='MNI', img_filters=[('desc', 'preproc')], slice_time_ref=0.0)
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

**Verification:**
```python
assert len(model._reporting_data['run_imgs']) == 4
```

### Step 10: Assign EXPECTED_FILENAME_ENDINGS = value

```python
EXPECTED_FILENAME_ENDINGS = ['sub-01_task-main_space-MNI_contrast-c0_stat-z_statmap.nii.gz', 'sub-01_task-main_space-MNI_contrast-c0_clusters.tsv', 'sub-01_task-main_space-MNI_contrast-c0_clusters.json', 'sub-01_ses-01_task-main_run-01_space-MNI_stat-rsquared_statmap.nii.gz', 'sub-01_ses-02_task-main_run-02_space-MNI_design.tsv', 'sub-01_ses-01_task-main_run-02_space-MNI_design.json', 'sub-01_task-main_space-MNI_mask.nii.gz']
```

### Step 11: Assign expected_keys = value

```python
expected_keys = ['Cluster size threshold (voxels)', 'Minimum distance (mm)']
```

### Step 12: Assign model = save_glm_to_bids(...)

```python
model = save_glm_to_bids(model=model, out_dir=tmp_path / 'output', contrasts=['c0'], **kwargs)
```

### Step 13: Call EXPECTED_FILENAME_ENDINGS.extend()

```python
EXPECTED_FILENAME_ENDINGS.extend(['sub-01_ses-02_task-main_run-01_space-MNI_design.png', 'sub-01_ses-02_task-main_run-01_space-MNI_corrdesign.png', 'sub-01_ses-01_task-main_run-02_space-MNI_contrast-c0_design.png'])
```

**Verification:**
```python
assert (tmp_path / 'output' / 'sub-01' / fname).exists()
```

### Step 14: Assign metadata = json.load(...)

```python
metadata = json.load(f)
```

### Step 15: Call expected_keys.extend()

```python
expected_keys.extend(['Height control', 'Threshold (computed)'])
```

### Step 16: Call expected_keys.extend()

```python
expected_keys.extend(['Height control', 'Threshold Z'])
```

**Verification:**
```python
assert key in metadata
```

### Step 17: Assign model = save_glm_to_bids(...)

```python
model = save_glm_to_bids(model=model, out_dir=tmp_path / 'output', contrasts=['c0'], **kwargs)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, kwargs

# Workflow
'Check that output filenames can be inferred from BIDS input.'
n_sub = 1
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=n_sub, n_ses=2, tasks=['main'], n_runs=[2], n_voxels=20)
models, imgs, events, _ = first_level_from_bids(dataset_path=bids_path, task_label='main', space_label='MNI', img_filters=[('desc', 'preproc')], slice_time_ref=0.0)
model = models[0]
run_imgs = imgs[0]
events = events[0]
model.minimize_memory = False
model.fit(run_imgs=run_imgs, events=events)
assert len(model._reporting_data['run_imgs']) == 4
if kwargs == {'height_control': None}:
    with pytest.warns(FutureWarning, match="the default 'threshold' will be set to"):
        model = save_glm_to_bids(model=model, out_dir=tmp_path / 'output', contrasts=['c0'], **kwargs)
else:
    model = save_glm_to_bids(model=model, out_dir=tmp_path / 'output', contrasts=['c0'], **kwargs)
EXPECTED_FILENAME_ENDINGS = ['sub-01_task-main_space-MNI_contrast-c0_stat-z_statmap.nii.gz', 'sub-01_task-main_space-MNI_contrast-c0_clusters.tsv', 'sub-01_task-main_space-MNI_contrast-c0_clusters.json', 'sub-01_ses-01_task-main_run-01_space-MNI_stat-rsquared_statmap.nii.gz', 'sub-01_ses-02_task-main_run-02_space-MNI_design.tsv', 'sub-01_ses-01_task-main_run-02_space-MNI_design.json', 'sub-01_task-main_space-MNI_mask.nii.gz']
if is_matplotlib_installed():
    EXPECTED_FILENAME_ENDINGS.extend(['sub-01_ses-02_task-main_run-01_space-MNI_design.png', 'sub-01_ses-02_task-main_run-01_space-MNI_corrdesign.png', 'sub-01_ses-01_task-main_run-02_space-MNI_contrast-c0_design.png'])
for fname in EXPECTED_FILENAME_ENDINGS:
    assert (tmp_path / 'output' / 'sub-01' / fname).exists()
with (tmp_path / 'output' / 'sub-01' / 'sub-01_task-main_space-MNI_contrast-c0_clusters.json').open('r') as f:
    metadata = json.load(f)
expected_keys = ['Cluster size threshold (voxels)', 'Minimum distance (mm)']
if 'height_control' not in kwargs:
    expected_keys.extend(['Height control', 'Threshold (computed)'])
else:
    expected_keys.extend(['Height control', 'Threshold Z'])
for key in expected_keys:
    assert key in metadata
```

## Next Steps


---

*Source: test_io.py:483 | Complexity: Advanced | Last updated: 2026-05-18*