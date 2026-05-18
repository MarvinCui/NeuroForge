# How To: Get Bids Files Fmriprep

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check proper number of files is returned for fmriprep version.

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
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Check proper number of files is returned for fmriprep version.'

```python
'Check proper number of files is returned for fmriprep version.'
```

**Verification:**
```python
assert len(selection) == 12 * n_sub
```

### Step 2: Assign n_sub = 2

```python
n_sub = 2
```

**Verification:**
```python
assert len(selection) == 12 * n_sub
```

### Step 3: Assign bids_path = create_fake_bids_dataset(...)

```python
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=n_sub, n_ses=2, tasks=['localizer', 'main'], n_runs=[1, 2], confounds_tag='desc-confounds_timeseries')
```

### Step 4: Assign selection = get_bids_files(...)

```python
selection = get_bids_files(bids_path / 'derivatives', file_tag='desc-confounds_timeseries')
```

**Verification:**
```python
assert len(selection) == 12 * n_sub
```

### Step 5: Assign bids_path = create_fake_bids_dataset(...)

```python
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=n_sub, n_ses=2, tasks=['localizer', 'main'], n_runs=[1, 2], confounds_tag='desc-confounds_regressors')
```

### Step 6: Assign selection = get_bids_files(...)

```python
selection = get_bids_files(bids_path / 'derivatives', file_tag='desc-confounds_regressors')
```

**Verification:**
```python
assert len(selection) == 12 * n_sub
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Check proper number of files is returned for fmriprep version.'
n_sub = 2
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=n_sub, n_ses=2, tasks=['localizer', 'main'], n_runs=[1, 2], confounds_tag='desc-confounds_timeseries')
selection = get_bids_files(bids_path / 'derivatives', file_tag='desc-confounds_timeseries')
assert len(selection) == 12 * n_sub
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=n_sub, n_ses=2, tasks=['localizer', 'main'], n_runs=[1, 2], confounds_tag='desc-confounds_regressors')
selection = get_bids_files(bids_path / 'derivatives', file_tag='desc-confounds_regressors')
assert len(selection) == 12 * n_sub
```

## Next Steps


---

*Source: test_query.py:298 | Complexity: Intermediate | Last updated: 2026-05-18*