# How To: Fmriprep Wf Heterogeneous Sessions

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: Test on a heterogeneous sessions layout, and test track_sessions behavior

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
# Fixtures: bids_root_factory
```

## Step-by-Step Guide

### Step 1: 'Test on a heterogeneous sessions layout, and test track_sessions behavior'

```python
'Test on a heterogeneous sessions layout, and test track_sessions behavior'
```

**Verification:**
```python
assert procs == [('01', ['anat', 'fmri'])]
```

### Step 2: Assign bids_dir = bids_root_factory(...)

```python
bids_dir = bids_root_factory('heterogeneous_sessions')
```

**Verification:**
```python
assert wf.get_node('sub_01_ses_anat-fmri_wf')
```

### Step 3: Assign config.workflow.bold2anat_init = 't1w'

```python
config.workflow.bold2anat_init = 't1w'
```

**Verification:**
```python
assert procs == [('01', None)]
```

### Step 4: Assign config.workflow.track_sessions = True

```python
config.workflow.track_sessions = True
```

**Verification:**
```python
assert wf.get_node('sub_01_wf')
```

### Step 5: Assign procs = config._create_processing_groups(...)

```python
procs = config._create_processing_groups()
```

**Verification:**
```python
assert procs == [('01', ['anat', 'fmri'])]
```

### Step 6: Assign wf = init_fmriprep_wf(...)

```python
wf = init_fmriprep_wf()
```

**Verification:**
```python
assert wf.get_node('sub_01_ses_anat-fmri_wf')
```

### Step 7: Assign config.workflow.track_sessions = False

```python
config.workflow.track_sessions = False
```

### Step 8: Assign procs = config._create_processing_groups(...)

```python
procs = config._create_processing_groups()
```

**Verification:**
```python
assert procs == [('01', None)]
```

### Step 9: Assign wf = init_fmriprep_wf(...)

```python
wf = init_fmriprep_wf()
```

**Verification:**
```python
assert wf.get_node('sub_01_wf')
```


## Complete Example

```python
# Setup
# Fixtures: bids_root_factory

# Workflow
'Test on a heterogeneous sessions layout, and test track_sessions behavior'
bids_dir = bids_root_factory('heterogeneous_sessions')
with mock_config(bids_dir=bids_dir):
    config.workflow.bold2anat_init = 't1w'
    config.workflow.track_sessions = True
    procs = config._create_processing_groups()
    assert procs == [('01', ['anat', 'fmri'])]
    wf = init_fmriprep_wf()
    assert wf.get_node('sub_01_ses_anat-fmri_wf')
    config.workflow.track_sessions = False
    procs = config._create_processing_groups()
    assert procs == [('01', None)]
    wf = init_fmriprep_wf()
    assert wf.get_node('sub_01_wf')
```

## Next Steps


---

*Source: test_base.py:362 | Complexity: Advanced | Last updated: 2026-05-18*