# How To: Get Metadata From Bids

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Ensure that metadata is correctly extracted from BIDS JSON files.

Throw a warning when the field is not found.
Throw a warning when there is no JSON file.

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

### Step 1: 'Ensure that metadata is correctly extracted from BIDS JSON files.\n\n    Throw a warning when the field is not found.\n    Throw a warning when there is no JSON file.\n    '

```python
'Ensure that metadata is correctly extracted from BIDS JSON files.\n\n    Throw a warning when the field is not found.\n    Throw a warning when there is no JSON file.\n    '
```

**Verification:**
```python
assert value == 2.0
```

### Step 2: Assign json_file = value

```python
json_file = tmp_path / 'sub-01_task-main_bold.json'
```

**Verification:**
```python
assert value is None
```

### Step 3: Assign json_files = value

```python
json_files = [json_file]
```

### Step 4: Assign value = _get_metadata_from_bids(...)

```python
value = _get_metadata_from_bids(field='RepetitionTime', json_files=json_files)
```

**Verification:**
```python
assert value == 2.0
```

### Step 5: Assign json_files = value

```python
json_files = []
```

### Step 6: Call json.dump()

```python
json.dump({'RepetitionTime': 2.0}, f)
```

### Step 7: Call json.dump()

```python
json.dump({'foo': 2.0}, f)
```

### Step 8: Assign value = _get_metadata_from_bids(...)

```python
value = _get_metadata_from_bids(field='RepetitionTime', json_files=json_files)
```

### Step 9: Assign value = _get_metadata_from_bids(...)

```python
value = _get_metadata_from_bids(field='RepetitionTime', json_files=json_files)
```

**Verification:**
```python
assert value is None
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Ensure that metadata is correctly extracted from BIDS JSON files.\n\n    Throw a warning when the field is not found.\n    Throw a warning when there is no JSON file.\n    '
json_file = tmp_path / 'sub-01_task-main_bold.json'
json_files = [json_file]
with json_file.open('w') as f:
    json.dump({'RepetitionTime': 2.0}, f)
value = _get_metadata_from_bids(field='RepetitionTime', json_files=json_files)
assert value == 2.0
with json_file.open('w') as f:
    json.dump({'foo': 2.0}, f)
with pytest.warns(RuntimeWarning, match="'RepetitionTime' not found"):
    value = _get_metadata_from_bids(field='RepetitionTime', json_files=json_files)
json_files = []
with pytest.warns(UserWarning, match='No .*json found in BIDS'):
    value = _get_metadata_from_bids(field='RepetitionTime', json_files=json_files)
    assert value is None
```

## Next Steps


---

*Source: test_query.py:36 | Complexity: Advanced | Last updated: 2026-05-18*