# How To: Fake Bids Extra Derivative Entity

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check files with extra entity are created appropriately.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `json`
- `numpy`
- `pandas`
- `pytest`
- `nibabel`
- `numpy.testing`
- `pandas.api.types`
- `pandas.testing`
- `nilearn._utils.data_gen`
- `nilearn.image`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Check files with extra entity are created appropriately.'

```python
'Check files with extra entity are created appropriately.'
```

**Verification:**
```python
assert not all_files
```

### Step 2: Assign n_sub = 2

```python
n_sub = 2
```

**Verification:**
```python
assert len(all_files) == n_derivatives_files_expected
```

### Step 3: Assign n_ses = 2

```python
n_ses = 2
```

### Step 4: Assign tasks = value

```python
tasks = ['main']
```

### Step 5: Assign n_runs = value

```python
n_runs = [2]
```

### Step 6: Assign entities = value

```python
entities = {'res': ['foo', 'bar']}
```

### Step 7: Assign bids_path = create_fake_bids_dataset(...)

```python
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=n_sub, n_ses=n_ses, tasks=tasks, n_runs=n_runs, entities=entities)
```

### Step 8: Assign all_files = list(...)

```python
all_files = list(bids_path.glob('sub-*/ses-*/*/*res*'))
```

**Verification:**
```python
assert not all_files
```

### Step 9: Assign all_files = list(...)

```python
all_files = list(bids_path.glob('derivatives/sub-*/ses-*/*/*'))
```

### Step 10: Assign n_derivatives_files_expected = value

```python
n_derivatives_files_expected = n_sub * (2 * sum(n_runs) * n_ses + 5 * sum(n_runs) * n_ses * len(entities['res']))
```

**Verification:**
```python
assert len(all_files) == n_derivatives_files_expected
```

### Step 11: Call _check_n_files_derivatives_for_task()

```python
_check_n_files_derivatives_for_task(bids_path=bids_path, n_sub=n_sub, n_ses=n_ses, task=task, n_run=n_run, extra_entity={'res': label})
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Check files with extra entity are created appropriately.'
n_sub = 2
n_ses = 2
tasks = ['main']
n_runs = [2]
entities = {'res': ['foo', 'bar']}
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=n_sub, n_ses=n_ses, tasks=tasks, n_runs=n_runs, entities=entities)
all_files = list(bids_path.glob('sub-*/ses-*/*/*res*'))
assert not all_files
for label in entities['res']:
    for task, n_run in zip(tasks, n_runs, strict=False):
        _check_n_files_derivatives_for_task(bids_path=bids_path, n_sub=n_sub, n_ses=n_ses, task=task, n_run=n_run, extra_entity={'res': label})
all_files = list(bids_path.glob('derivatives/sub-*/ses-*/*/*'))
n_derivatives_files_expected = n_sub * (2 * sum(n_runs) * n_ses + 5 * sum(n_runs) * n_ses * len(entities['res']))
assert len(all_files) == n_derivatives_files_expected
```

## Next Steps


---

*Source: test_data_gen.py:428 | Complexity: Advanced | Last updated: 2026-05-18*