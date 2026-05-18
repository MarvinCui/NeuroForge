# How To: Bold Wf

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: mock, pytest, workflow, integration

## Overview

Workflow: Test as many combinations of precomputed files and input
configurations as possible.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `nibabel`
- `numpy`
- `pytest`
- `nipype.pipeline.engine.utils`
- `niworkflows.utils.testing`
- `tests`
- `tests.layouts`
- `base`
- `logging`

**Setup Required:**
```python
# Fixtures: bids_root, tmp_path, task, fieldmap_id, freesurfer, level, bold2anat_init
```

## Step-by-Step Guide

### Step 1: 'Test as many combinations of precomputed files and input\n    configurations as possible.'

```python
'Test as many combinations of precomputed files and input\n    configurations as possible.'
```

### Step 2: Assign output_dir = value

```python
output_dir = tmp_path / 'output'
```

### Step 3: Call output_dir.mkdir()

```python
output_dir.mkdir()
```

### Step 4: Assign img = nb.Nifti1Image(...)

```python
img = nb.Nifti1Image(np.zeros((10, 10, 10, 10)), np.eye(4))
```

### Step 5: Call img.to_filename()

```python
img.to_filename(sbref)
```

### Step 6: Assign flatgraph = wf._create_flat_graph(...)

```python
flatgraph = wf._create_flat_graph()
```

### Step 7: Call generate_expanded_graph()

```python
generate_expanded_graph(flatgraph)
```

### Step 8: Assign bold_series = value

```python
bold_series = [str(bids_root / 'sub-01' / 'func' / 'sub-01_task-rest_run-1_bold.nii.gz')]
```

### Step 9: Assign sbref = str(...)

```python
sbref = str(bids_root / 'sub-01' / 'func' / 'sub-01_task-rest_run-1_sbref.nii.gz')
```

### Step 10: Call img.to_filename()

```python
img.to_filename(path)
```

### Step 11: Assign config.workflow.bold2anat_init = bold2anat_init

```python
config.workflow.bold2anat_init = bold2anat_init
```

### Step 12: Assign config.workflow.level = level

```python
config.workflow.level = level
```

### Step 13: Assign config.workflow.run_reconall = freesurfer

```python
config.workflow.run_reconall = freesurfer
```

### Step 14: Assign wf = init_bold_wf(...)

```python
wf = init_bold_wf(bold_series=bold_series, fieldmap_id=fieldmap_id, precomputed={})
```

### Step 15: Assign bold_series = value

```python
bold_series = [str(bids_root / 'sub-01' / 'func' / f'sub-01_task-nback_echo-{i}_bold.nii.gz') for i in range(1, 4)]
```

### Step 16: Assign sbref = str(...)

```python
sbref = str(bids_root / 'sub-01' / 'func' / 'sub-01_task-nback_echo-1_sbref.nii.gz')
```


## Complete Example

```python
# Setup
# Fixtures: bids_root, tmp_path, task, fieldmap_id, freesurfer, level, bold2anat_init

# Workflow
'Test as many combinations of precomputed files and input\n    configurations as possible.'
output_dir = tmp_path / 'output'
output_dir.mkdir()
img = nb.Nifti1Image(np.zeros((10, 10, 10, 10)), np.eye(4))
if task == 'rest':
    bold_series = [str(bids_root / 'sub-01' / 'func' / 'sub-01_task-rest_run-1_bold.nii.gz')]
    sbref = str(bids_root / 'sub-01' / 'func' / 'sub-01_task-rest_run-1_sbref.nii.gz')
elif task == 'nback':
    bold_series = [str(bids_root / 'sub-01' / 'func' / f'sub-01_task-nback_echo-{i}_bold.nii.gz') for i in range(1, 4)]
    sbref = str(bids_root / 'sub-01' / 'func' / 'sub-01_task-nback_echo-1_sbref.nii.gz')
for path in bold_series:
    img.to_filename(path)
img.to_filename(sbref)
with mock_config(bids_dir=bids_root):
    config.workflow.bold2anat_init = bold2anat_init
    config.workflow.level = level
    config.workflow.run_reconall = freesurfer
    wf = init_bold_wf(bold_series=bold_series, fieldmap_id=fieldmap_id, precomputed={})
flatgraph = wf._create_flat_graph()
generate_expanded_graph(flatgraph)
```

## Next Steps


---

*Source: test_base.py:39 | Complexity: Advanced | Last updated: 2026-05-18*