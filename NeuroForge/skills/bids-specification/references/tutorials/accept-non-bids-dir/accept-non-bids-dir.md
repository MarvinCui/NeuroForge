# How To: Accept Non Bids Dir

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test accept non bids dir

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
assert len(result['path_tracking']) == 0
```

### Step 2: Assign dataset_reference = os.path.join(...)

```python
dataset_reference = os.path.join(bids_examples, dataset)
```

### Step 3: Assign tmp_path = str(...)

```python
tmp_path = str(tmp_path)
```

### Step 4: Call shutil.copytree()

```python
shutil.copytree(dataset_reference, tmp_path, dirs_exist_ok=True)
```

### Step 5: Call os.remove()

```python
os.remove(os.path.join(tmp_path, 'dataset_description.json'))
```

### Step 6: Assign result = validate_bids(...)

```python
result = validate_bids(tmp_path, accept_non_bids_dir=True)
```

**Verification:**
```python
assert len(result['path_tracking']) == 0
```

### Step 7: Assign _ = validate_bids(...)

```python
_ = validate_bids(tmp_path)
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
os.remove(os.path.join(tmp_path, 'dataset_description.json'))
with pytest.raises(ValueError, match='None of the files in the input list are part of a BIDS dataset. Aborting.'):
    _ = validate_bids(tmp_path)
result = validate_bids(tmp_path, accept_non_bids_dir=True)
assert len(result['path_tracking']) == 0
```

## Next Steps


---

*Source: test_validator.py:216 | Complexity: Intermediate | Last updated: 2026-05-18*