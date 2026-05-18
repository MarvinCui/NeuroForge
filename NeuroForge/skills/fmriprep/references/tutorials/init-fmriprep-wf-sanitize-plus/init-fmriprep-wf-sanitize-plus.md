# How To: Init Fmriprep Wf Sanitize Plus

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test init fmriprep wf sanitize plus

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

### Step 2: Assign spec = get_layout(...)

```python
spec = get_layout('no_session')
```

### Step 3: Assign unknown = 'mb4+pf68th'

```python
spec['01']['func'][0]['acquisition'] = 'mb4+pf68th'
```

### Step 4: Assign unknown = 'memprage+rms'

```python
spec['01']['anat'][0]['acquisition'] = 'memprage+rms'
```

### Step 5: Assign unknown = 'memprage'

```python
spec['01']['anat'][1]['acquisition'] = 'memprage'
```

### Step 6: Assign unknown = 'sbref+pf68th'

```python
spec['01']['fmap'][2]['acquisition'] = 'sbref+pf68th'
```

### Step 7: Assign unknown = 'sbref+pf68th'

```python
spec['01']['fmap'][3]['acquisition'] = 'sbref+pf68th'
```

### Step 8: Call generate_bids_skeleton()

```python
generate_bids_skeleton(bids_dir, spec)
```

### Step 9: Assign img = nb.Nifti1Image(...)

```python
img = nb.Nifti1Image(np.zeros((10, 10, 10, 10)), np.eye(4))
```

### Step 10: Call generate_expanded_graph()

```python
generate_expanded_graph(wf._create_flat_graph())
```

### Step 11: Call img.to_filename()

```python
img.to_filename(img_path)
```

### Step 12: Assign wf = init_fmriprep_wf(...)

```python
wf = init_fmriprep_wf()
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
bids_dir = tmp_path / 'bids'
spec = get_layout('no_session')
spec['01']['func'][0]['acquisition'] = 'mb4+pf68th'
spec['01']['anat'][0]['acquisition'] = 'memprage+rms'
spec['01']['anat'][1]['acquisition'] = 'memprage'
spec['01']['fmap'][2]['acquisition'] = 'sbref+pf68th'
spec['01']['fmap'][3]['acquisition'] = 'sbref+pf68th'
del spec['01']['func'][4:]
generate_bids_skeleton(bids_dir, spec)
img = nb.Nifti1Image(np.zeros((10, 10, 10, 10)), np.eye(4))
for img_path in bids_dir.glob('sub-01/*/*.nii.gz'):
    img.to_filename(img_path)
with mock_config(bids_dir=bids_dir):
    wf = init_fmriprep_wf()
generate_expanded_graph(wf._create_flat_graph())
```

## Next Steps


---

*Source: test_base.py:220 | Complexity: Advanced | Last updated: 2026-05-18*