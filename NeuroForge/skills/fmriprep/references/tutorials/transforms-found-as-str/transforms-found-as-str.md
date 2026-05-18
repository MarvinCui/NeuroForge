# How To: Transforms Found As Str

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test transforms found as str

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `pytest`
- `fmriprep.utils`

**Setup Required:**
```python
# Fixtures: tmp_path, xfm
```

## Step-by-Step Guide

### Step 1: Assign subject = '0'

```python
subject = '0'
```

**Verification:**
```python
assert derivs == {'transforms': {xfm: str(to_find)}}
```

### Step 2: Assign task = 'rest'

```python
task = 'rest'
```

### Step 3: Assign fromto = value

```python
fromto = {'hmc': 'from-orig_to-boldref', 'boldref2fmap': 'from-boldref_to-auto00000', 'boldref2anat': 'from-boldref_to-anat'}[xfm]
```

### Step 4: Assign to_find = tmp_path.joinpath(...)

```python
to_find = tmp_path.joinpath(f'sub-{subject}', 'func', f'sub-{subject}_task-{task}_{fromto}_mode-image_xfm.txt')
```

### Step 5: Call to_find.parent.mkdir()

```python
to_find.parent.mkdir(parents=True)
```

### Step 6: Call to_find.touch()

```python
to_find.touch()
```

### Step 7: Assign entities = value

```python
entities = {'subject': subject, 'task': task, 'suffix': 'bold', 'extension': '.nii.gz'}
```

### Step 8: Assign derivs = bids.collect_derivatives(...)

```python
derivs = bids.collect_derivatives(derivatives_dir=tmp_path, entities=entities, fieldmap_id='auto_00000')
```

**Verification:**
```python
assert derivs == {'transforms': {xfm: str(to_find)}}
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, xfm

# Workflow
subject = '0'
task = 'rest'
fromto = {'hmc': 'from-orig_to-boldref', 'boldref2fmap': 'from-boldref_to-auto00000', 'boldref2anat': 'from-boldref_to-anat'}[xfm]
to_find = tmp_path.joinpath(f'sub-{subject}', 'func', f'sub-{subject}_task-{task}_{fromto}_mode-image_xfm.txt')
to_find.parent.mkdir(parents=True)
to_find.touch()
entities = {'subject': subject, 'task': task, 'suffix': 'bold', 'extension': '.nii.gz'}
derivs = bids.collect_derivatives(derivatives_dir=tmp_path, entities=entities, fieldmap_id='auto_00000')
assert derivs == {'transforms': {xfm: str(to_find)}}
```

## Next Steps


---

*Source: test_derivative_cache.py:31 | Complexity: Advanced | Last updated: 2026-05-18*