# How To: Get Estimator B0Field And Intendedfor

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test get estimator b0field and intendedfor

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
assert get_estimator(layout, bold_files[0]) == ('epi',)
```

### Step 2: Assign spec = get_layout(...)

```python
spec = get_layout('no_session')
```

**Verification:**
```python
assert get_estimator(layout, bold_files[1]) == ()
```

### Step 3: Assign unknown = 'epi'

```python
spec['01']['func'][0]['metadata']['B0FieldSource'] = 'epi'
```

### Step 4: Assign unknown = 'epi'

```python
spec['01']['fmap'][2]['metadata']['B0FieldIdentifier'] = 'epi'
```

### Step 5: Assign unknown = 'epi'

```python
spec['01']['fmap'][3]['metadata']['B0FieldIdentifier'] = 'epi'
```

### Step 6: Assign unknown = 'func/sub-01_task-rest_run-2_bold.nii.gz'

```python
spec['01']['fmap'][0]['metadata']['IntendedFor'] = 'func/sub-01_task-rest_run-2_bold.nii.gz'
```

### Step 7: Call generate_bids_skeleton()

```python
generate_bids_skeleton(bids_dir, spec)
```

### Step 8: Assign layout = bids.BIDSLayout(...)

```python
layout = bids.BIDSLayout(bids_dir)
```

### Step 9: Assign _ = find_estimators(...)

```python
_ = find_estimators(layout=layout, subject='01')
```

### Step 10: Assign bold_files = sorted(...)

```python
bold_files = sorted(layout.get(suffix='bold', task='rest', extension='.nii.gz', return_type='file'))
```

**Verification:**
```python
assert get_estimator(layout, bold_files[0]) == ('epi',)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
bids_dir = tmp_path / 'bids'
spec = get_layout('no_session')
spec['01']['func'][0]['metadata']['B0FieldSource'] = 'epi'
spec['01']['fmap'][2]['metadata']['B0FieldIdentifier'] = 'epi'
spec['01']['fmap'][3]['metadata']['B0FieldIdentifier'] = 'epi'
spec['01']['fmap'][0]['metadata']['IntendedFor'] = 'func/sub-01_task-rest_run-2_bold.nii.gz'
generate_bids_skeleton(bids_dir, spec)
layout = bids.BIDSLayout(bids_dir)
_ = find_estimators(layout=layout, subject='01')
bold_files = sorted(layout.get(suffix='bold', task='rest', extension='.nii.gz', return_type='file'))
assert get_estimator(layout, bold_files[0]) == ('epi',)
assert get_estimator(layout, bold_files[1]) == ()
```

## Next Steps


---

*Source: test_base.py:255 | Complexity: Advanced | Last updated: 2026-05-18*