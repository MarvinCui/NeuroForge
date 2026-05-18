# How To: Bids Dataset No Session

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: n_ses = 0 prevent creation of a session folder.

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

### Step 1: 'n_ses = 0 prevent creation of a session folder.'

```python
'n_ses = 0 prevent creation of a session folder.'
```

**Verification:**
```python
assert not files
```

### Step 2: Assign bids_path = create_fake_bids_dataset(...)

```python
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=1, n_ses=0, tasks=['main'], n_runs=[1], with_derivatives=True)
```

**Verification:**
```python
assert len(files) == 5
```

### Step 3: Assign files = list(...)

```python
files = list(bids_path.glob('**/*ses-*'))
```

**Verification:**
```python
assert len(files) == 1
```

### Step 4: Assign files = list(...)

```python
files = list(bids_path.glob('**/*.nii.gz'))
```

**Verification:**
```python
assert len(files) == 5
```

### Step 5: Assign files = list(...)

```python
files = list(bids_path.glob(f'**/*{suffix}'))
```

**Verification:**
```python
assert len(files) == 1
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'n_ses = 0 prevent creation of a session folder.'
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=1, n_ses=0, tasks=['main'], n_runs=[1], with_derivatives=True)
files = list(bids_path.glob('**/*ses-*'))
assert not files
files = list(bids_path.glob('**/*.nii.gz'))
assert len(files) == 5
for suffix in ['events.tsv', 'timeseries.tsv', 'bold.json']:
    files = list(bids_path.glob(f'**/*{suffix}'))
    assert len(files) == 1
```

## Next Steps


---

*Source: test_data_gen.py:285 | Complexity: Intermediate | Last updated: 2026-05-18*