# How To: Get Estimator Intendedfor

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test get estimator intendedfor

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `unittest.mock`
- `bids`
- `nibabel`
- `numpy`
- `pytest`
- `nipype.pipeline.engine.utils`
- `niworkflows.utils.testing`
- `sdcflows.fieldmaps`
- `sdcflows.utils.wrangler`
- `base`
- `tests`
- `layouts`
- `logging`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: Assign bids_dir = value

```python
bids_dir = tmp_path / 'bids'
```

**Verification:**
```python
assert get_estimator(layout, bold_files[1]) == ('auto_00000',)
```

### Step 2: Assign spec = get_layout(...)

```python
spec = get_layout('no_session')
```

### Step 3: Assign unknown = 'func/sub-01_task-rest_run-2_bold.nii.gz'

```python
spec['01']['fmap'][0]['metadata']['IntendedFor'] = 'func/sub-01_task-rest_run-2_bold.nii.gz'
```

### Step 4: Call generate_bids_skeleton()

```python
generate_bids_skeleton(bids_dir, spec)
```

### Step 5: Assign layout = bids.BIDSLayout(...)

```python
layout = bids.BIDSLayout(bids_dir)
```

### Step 6: Assign _ = find_estimators(...)

```python
_ = find_estimators(layout=layout, subject='01')
```

### Step 7: Assign bold_files = sorted(...)

```python
bold_files = sorted(layout.get(suffix='bold', task='rest', extension='.nii.gz', return_type='file'))
```

**Verification:**
```python
assert get_estimator(layout, bold_files[1]) == ('auto_00000',)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
bids_dir = tmp_path / 'bids'
spec = get_layout('no_session')
spec['01']['fmap'][0]['metadata']['IntendedFor'] = 'func/sub-01_task-rest_run-2_bold.nii.gz'
generate_bids_skeleton(bids_dir, spec)
layout = bids.BIDSLayout(bids_dir)
_ = find_estimators(layout=layout, subject='01')
bold_files = sorted(layout.get(suffix='bold', task='rest', extension='.nii.gz', return_type='file'))
assert get_estimator(layout, bold_files[1]) == ('auto_00000',)
```

## Next Steps


---

*Source: test_base.py:280 | Complexity: Intermediate | Last updated: 2026-05-18*