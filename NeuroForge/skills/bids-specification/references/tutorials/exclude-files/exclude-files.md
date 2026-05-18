# How To: Exclude Files

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test exclude files

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `shutil`
- `pytest`
- `bidsschematools.conftest`
- `bidsschematools.validator`
- `data`
- `data`
- `bidsschematools.validator`
- `bidsschematools.validator`
- `bidsschematools.validator`
- `bidsschematools`

**Setup Required:**
```python
# Fixtures: bids_examples, tmp_path
```

## Step-by-Step Guide

### Step 1: Assign dataset = 'asl003'

```python
dataset = 'asl003'
```

**Verification:**
```python
assert len(result['path_tracking']) == 1
```

### Step 2: Assign dataset_reference = os.path.join(...)

```python
dataset_reference = os.path.join(bids_examples, dataset)
```

**Verification:**
```python
assert len(result['path_tracking']) == 0
```

### Step 3: Assign tmp_path = str(...)

```python
tmp_path = str(tmp_path)
```

### Step 4: Call shutil.copytree()

```python
shutil.copytree(dataset_reference, tmp_path, dirs_exist_ok=True)
```

### Step 5: Assign archive_file_name = 'dandiset.yaml'

```python
archive_file_name = 'dandiset.yaml'
```

### Step 6: Assign archive_file_path = os.path.join(...)

```python
archive_file_path = os.path.join(tmp_path, archive_file_name)
```

### Step 7: Assign result = validate_bids(...)

```python
result = validate_bids(tmp_path)
```

**Verification:**
```python
assert len(result['path_tracking']) == 1
```

### Step 8: Assign result = validate_bids(...)

```python
result = validate_bids(tmp_path, exclude_files=[archive_file_name])
```

**Verification:**
```python
assert len(result['path_tracking']) == 0
```

### Step 9: Call f.write()

```python
f.write(' \n')
```


## Complete Example

```python
# Setup
# Fixtures: bids_examples, tmp_path

# Workflow
from bidsschematools.validator import validate_bids
dataset = 'asl003'
dataset_reference = os.path.join(bids_examples, dataset)
tmp_path = str(tmp_path)
shutil.copytree(dataset_reference, tmp_path, dirs_exist_ok=True)
archive_file_name = 'dandiset.yaml'
archive_file_path = os.path.join(tmp_path, archive_file_name)
with open(archive_file_path, 'w') as f:
    f.write(' \n')
result = validate_bids(tmp_path)
assert len(result['path_tracking']) == 1
result = validate_bids(tmp_path, exclude_files=[archive_file_name])
assert len(result['path_tracking']) == 0
```

## Next Steps


---

*Source: test_validator.py:189 | Complexity: Advanced | Last updated: 2026-05-18*