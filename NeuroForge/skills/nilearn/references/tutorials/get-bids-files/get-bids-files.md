# How To: Get Bids Files

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check proper number of files is returned.

For each possible option of file selection
we check that we recover the appropriate amount of files,
as included in the fake bids dataset.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `json`
- `pathlib`
- `pytest`
- `nilearn._utils.data_gen`
- `nilearn.interfaces.bids.query`

**Setup Required:**
```python
# Fixtures: tmp_path, params, files_per_subject
```

## Step-by-Step Guide

### Step 1: 'Check proper number of files is returned.\n\n    For each possible option of file selection\n    we check that we recover the appropriate amount of files,\n    as included in the fake bids dataset.\n    '

```python
'Check proper number of files is returned.\n\n    For each possible option of file selection\n    we check that we recover the appropriate amount of files,\n    as included in the fake bids dataset.\n    '
```

**Verification:**
```python
assert len(selection) == files_per_subject * n_sub
```

### Step 2: Assign n_sub = 2

```python
n_sub = 2
```

**Verification:**
```python
assert len(selection) == 19
```

### Step 3: Assign bids_path = create_fake_bids_dataset(...)

```python
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=n_sub, n_ses=2, tasks=['localizer', 'main'], n_runs=[1, 2])
```

**Verification:**
```python
assert len(selection) == 1
```

### Step 4: Assign selection = get_bids_files(...)

```python
selection = get_bids_files(bids_path, **params)
```

**Verification:**
```python
assert len(selection) == files_per_subject * n_sub
```

### Step 5: Assign selection = get_bids_files(...)

```python
selection = get_bids_files(bids_path, sub_label='01')
```

**Verification:**
```python
assert len(selection) == 19
```

### Step 6: Assign selection = get_bids_files(...)

```python
selection = get_bids_files(bids_path, sub_folder=False)
```

**Verification:**
```python
assert len(selection) == 1
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, params, files_per_subject

# Workflow
'Check proper number of files is returned.\n\n    For each possible option of file selection\n    we check that we recover the appropriate amount of files,\n    as included in the fake bids dataset.\n    '
n_sub = 2
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=n_sub, n_ses=2, tasks=['localizer', 'main'], n_runs=[1, 2])
selection = get_bids_files(bids_path, **params)
assert len(selection) == files_per_subject * n_sub
selection = get_bids_files(bids_path, sub_label='01')
assert len(selection) == 19
selection = get_bids_files(bids_path, sub_folder=False)
assert len(selection) == 1
```

## Next Steps


---

*Source: test_query.py:266 | Complexity: Intermediate | Last updated: 2026-05-18*