# How To: Add Metadata To Bids Derivatives With Json Path

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test add metadata to bids derivatives with json path

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

### Step 1: Assign target_dir = value

```python
target_dir = tmp_path / 'derivatives' / 'sub-02'
```

**Verification:**
```python
assert json_file.exists()
```

### Step 2: Call target_dir.mkdir()

```python
target_dir.mkdir(parents=True)
```

**Verification:**
```python
assert json_file.name == 'sub-02_task-main_bold.json'
```

### Step 3: Assign json_file = 'derivatives/sub-02/sub-02_task-main_bold.json'

```python
json_file = 'derivatives/sub-02/sub-02_task-main_bold.json'
```

**Verification:**
```python
assert metadata == {'foo': 'bar'}
```

### Step 4: Assign json_file = add_metadata_to_bids_dataset(...)

```python
json_file = add_metadata_to_bids_dataset(bids_path=tmp_path, metadata={'foo': 'bar'}, json_file=json_file)
```

**Verification:**
```python
assert json_file.exists()
```

### Step 5: Assign metadata = json.load(...)

```python
metadata = json.load(f)
```

**Verification:**
```python
assert metadata == {'foo': 'bar'}
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
target_dir = tmp_path / 'derivatives' / 'sub-02'
target_dir.mkdir(parents=True)
json_file = 'derivatives/sub-02/sub-02_task-main_bold.json'
json_file = add_metadata_to_bids_dataset(bids_path=tmp_path, metadata={'foo': 'bar'}, json_file=json_file)
assert json_file.exists()
assert json_file.name == 'sub-02_task-main_bold.json'
with json_file.open() as f:
    metadata = json.load(f)
    assert metadata == {'foo': 'bar'}
```

## Next Steps


---

*Source: test_data_gen.py:51 | Complexity: Intermediate | Last updated: 2026-05-18*