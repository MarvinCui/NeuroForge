# How To: Fake Bids Raw With Session And Runs

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check number of each file 'type' created in raw.

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
# Fixtures: tmp_path, n_sub, n_ses, tasks, n_runs
```

## Step-by-Step Guide

### Step 1: "Check number of each file 'type' created in raw."

```python
"Check number of each file 'type' created in raw."
```

**Verification:**
```python
assert len(raw_anat_files) == n_sub
```

### Step 2: Assign bids_path = create_fake_bids_dataset(...)

```python
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=n_sub, n_ses=n_ses, tasks=tasks, n_runs=n_runs)
```

**Verification:**
```python
assert len(files) == n_sub * n_ses * n_runs[i]
```

### Step 3: Assign file_pattern = 'sub-*/ses-*/anat/sub-*ses-*T1w.nii.gz'

```python
file_pattern = 'sub-*/ses-*/anat/sub-*ses-*T1w.nii.gz'
```

**Verification:**
```python
assert len(all_files) == n_raw_files_expected
```

### Step 4: Assign raw_anat_files = list(...)

```python
raw_anat_files = list(bids_path.glob(file_pattern))
```

**Verification:**
```python
assert len(raw_anat_files) == n_sub
```

### Step 5: Assign all_files = list(...)

```python
all_files = list(bids_path.glob('sub-*/ses-*/*/*'))
```

### Step 6: Assign n_raw_files_expected = value

```python
n_raw_files_expected = n_sub * (1 + 3 * sum(n_runs) * n_ses)
```

**Verification:**
```python
assert len(all_files) == n_raw_files_expected
```

### Step 7: Assign file_pattern = _bids_path_template(...)

```python
file_pattern = _bids_path_template(task=task, suffix=suffix, n_runs=n_runs[i])
```

### Step 8: Assign files = list(...)

```python
files = list(bids_path.glob(file_pattern))
```

**Verification:**
```python
assert len(files) == n_sub * n_ses * n_runs[i]
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, n_sub, n_ses, tasks, n_runs

# Workflow
"Check number of each file 'type' created in raw."
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=n_sub, n_ses=n_ses, tasks=tasks, n_runs=n_runs)
file_pattern = 'sub-*/ses-*/anat/sub-*ses-*T1w.nii.gz'
raw_anat_files = list(bids_path.glob(file_pattern))
assert len(raw_anat_files) == n_sub
for i, task in enumerate(tasks):
    for suffix in ['bold.nii.gz', 'bold.json', 'events.tsv']:
        file_pattern = _bids_path_template(task=task, suffix=suffix, n_runs=n_runs[i])
        files = list(bids_path.glob(file_pattern))
        assert len(files) == n_sub * n_ses * n_runs[i]
all_files = list(bids_path.glob('sub-*/ses-*/*/*'))
n_raw_files_expected = n_sub * (1 + 3 * sum(n_runs) * n_ses)
assert len(all_files) == n_raw_files_expected
```

## Next Steps


---

*Source: test_data_gen.py:137 | Complexity: Advanced | Last updated: 2026-05-18*