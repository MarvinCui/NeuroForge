# How To: Baseline Found As Str

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test baseline found as str

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `pytest`
- `fmriprep.utils`

**Setup Required:**
```python
# Fixtures: tmp_path, desc
```

## Step-by-Step Guide

### Step 1: Assign subject = '0'

```python
subject = '0'
```

**Verification:**
```python
assert dict(derivs) == {f'{desc}_boldref': str(to_find), 'transforms': {}}
```

### Step 2: Assign task = 'rest'

```python
task = 'rest'
```

### Step 3: Assign to_find = tmp_path.joinpath(...)

```python
to_find = tmp_path.joinpath(f'sub-{subject}', 'func', f'sub-{subject}_task-{task}_desc-{desc}_boldref.nii.gz')
```

### Step 4: Call to_find.parent.mkdir()

```python
to_find.parent.mkdir(parents=True)
```

### Step 5: Call to_find.touch()

```python
to_find.touch()
```

### Step 6: Assign entities = value

```python
entities = {'subject': subject, 'task': task, 'suffix': 'bold', 'extension': '.nii.gz'}
```

### Step 7: Assign derivs = bids.collect_derivatives(...)

```python
derivs = bids.collect_derivatives(derivatives_dir=tmp_path, entities=entities)
```

**Verification:**
```python
assert dict(derivs) == {f'{desc}_boldref': str(to_find), 'transforms': {}}
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, desc

# Workflow
subject = '0'
task = 'rest'
to_find = tmp_path.joinpath(f'sub-{subject}', 'func', f'sub-{subject}_task-{task}_desc-{desc}_boldref.nii.gz')
to_find.parent.mkdir(parents=True)
to_find.touch()
entities = {'subject': subject, 'task': task, 'suffix': 'bold', 'extension': '.nii.gz'}
derivs = bids.collect_derivatives(derivatives_dir=tmp_path, entities=entities)
assert dict(derivs) == {f'{desc}_boldref': str(to_find), 'transforms': {}}
```

## Next Steps


---

*Source: test_derivative_cache.py:9 | Complexity: Intermediate | Last updated: 2026-05-18*