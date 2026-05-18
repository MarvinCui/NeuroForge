# How To: Bold Native Precomputes

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
- `fit`
- `logging`

**Setup Required:**
```python
# Fixtures: bids_root, tmp_path, task, fieldmap_id, run_stc
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

### Step 5: Assign flatgraph = wf._create_flat_graph(...)

```python
flatgraph = wf._create_flat_graph()
```

### Step 6: Call generate_expanded_graph()

```python
generate_expanded_graph(flatgraph)
```

### Step 7: Assign bold_series = value

```python
bold_series = [str(bids_root / 'sub-01' / 'func' / 'sub-01_task-rest_run-1_bold.nii.gz')]
```

### Step 8: Call img.to_filename()

```python
img.to_filename(path)
```

### Step 9: Assign config.workflow.ignore = value

```python
config.workflow.ignore = ['slicetiming'] if not run_stc else []
```

### Step 10: Assign wf = init_bold_native_wf(...)

```python
wf = init_bold_native_wf(bold_series=bold_series, fieldmap_id=fieldmap_id, omp_nthreads=1)
```

### Step 11: Assign bold_series = value

```python
bold_series = [str(bids_root / 'sub-01' / 'func' / f'sub-01_task-nback_echo-{i}_bold.nii.gz') for i in range(1, 4)]
```


## Complete Example

```python
# Setup
# Fixtures: bids_root, tmp_path, task, fieldmap_id, run_stc

# Workflow
'Test as many combinations of precomputed files and input\n    configurations as possible.'
output_dir = tmp_path / 'output'
output_dir.mkdir()
img = nb.Nifti1Image(np.zeros((10, 10, 10, 10)), np.eye(4))
if task == 'rest':
    bold_series = [str(bids_root / 'sub-01' / 'func' / 'sub-01_task-rest_run-1_bold.nii.gz')]
elif task == 'nback':
    bold_series = [str(bids_root / 'sub-01' / 'func' / f'sub-01_task-nback_echo-{i}_bold.nii.gz') for i in range(1, 4)]
for path in bold_series:
    img.to_filename(path)
with mock_config(bids_dir=bids_root):
    config.workflow.ignore = ['slicetiming'] if not run_stc else []
    wf = init_bold_native_wf(bold_series=bold_series, fieldmap_id=fieldmap_id, omp_nthreads=1)
flatgraph = wf._create_flat_graph()
generate_expanded_graph(flatgraph)
```

## Next Steps


---

*Source: test_fit.py:140 | Complexity: Advanced | Last updated: 2026-05-18*