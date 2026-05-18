# How To: Bidssourcefile

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test the BIDSSourceFile interface

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pytest`
- `fmriprep.interfaces.bids`
- `fmriprep.interfaces.bids`

**Setup Required:**
```python
# Fixtures: bids_info_anat, bids_info_func, precomputed_infos
```

## Step-by-Step Guide

### Step 1: 'Test the BIDSSourceFile interface'

```python
'Test the BIDSSourceFile interface'
```

**Verification:**
```python
assert results.outputs.source_file == bold
```

### Step 2: Assign interface = BIDSSourceFile(...)

```python
interface = BIDSSourceFile()
```

**Verification:**
```python
assert results.outputs.source_file == bids_info_anat[anat_type][0]
```

### Step 3: Assign anat_type = next(...)

```python
anat_type = next(iter(bids_info_anat))
```

### Step 4: Assign interface.inputs.anat_type = anat_type

```python
interface.inputs.anat_type = anat_type
```

### Step 5: Assign interface.inputs.bids_info = value

```python
interface.inputs.bids_info = {**bids_info_anat, **bids_info_func}
```

### Step 6: Assign interface.inputs.precomputed = precomputed_infos

```python
interface.inputs.precomputed = precomputed_infos
```

### Step 7: Assign results = interface.run(...)

```python
results = interface.run()
```

### Step 8: Assign bold = value

```python
bold = 'sub-01/func/sub-01_bold.nii.gz' if isinstance(bids_info_func['bold'][0], list) else 'sub-01/func/sub-01_task-rest_bold.nii.gz'
```

**Verification:**
```python
assert results.outputs.source_file == bold
```


## Complete Example

```python
# Setup
# Fixtures: bids_info_anat, bids_info_func, precomputed_infos

# Workflow
'Test the BIDSSourceFile interface'
from fmriprep.interfaces.bids import BIDSSourceFile
interface = BIDSSourceFile()
anat_type = next(iter(bids_info_anat))
interface.inputs.anat_type = anat_type
interface.inputs.bids_info = {**bids_info_anat, **bids_info_func}
interface.inputs.precomputed = precomputed_infos
results = interface.run()
if precomputed_infos:
    bold = 'sub-01/func/sub-01_bold.nii.gz' if isinstance(bids_info_func['bold'][0], list) else 'sub-01/func/sub-01_task-rest_bold.nii.gz'
    assert results.outputs.source_file == bold
else:
    assert results.outputs.source_file == bids_info_anat[anat_type][0]
```

## Next Steps


---

*Source: test_bids.py:114 | Complexity: Advanced | Last updated: 2026-05-18*