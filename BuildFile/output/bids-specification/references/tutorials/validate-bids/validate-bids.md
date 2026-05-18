# How To: Validate Bids

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test validate bids

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

### Step 1: Assign selected_dir = os.path.join(...)

```python
selected_dir = os.path.join(bids_examples, BIDS_SELECTION[0])
```

**Verification:**
```python
assert len(result['path_tracking']) == 0
```

### Step 2: Assign selected_paths = value

```python
selected_paths = []
```

**Verification:**
```python
assert result['bids_version'] == expected_version
```

### Step 3: Assign result = validate_bids(...)

```python
result = validate_bids(selected_paths, schema_path=False)
```

### Step 4: Assign result = validate_bids(...)

```python
result = validate_bids(selected_paths, report_path=True)
```

### Step 5: Assign result = validate_bids(...)

```python
result = validate_bids(selected_paths, report_path=os.path.join(tmp_path, 'test_bids.log'))
```

**Verification:**
```python
assert len(result['path_tracking']) == 0
```

### Step 6: Assign schema_path = load.readable(...)

```python
schema_path = load.readable('schema')
```

### Step 7: Assign expected_version = schema_path.joinpath.read_text.rstrip(...)

```python
expected_version = schema_path.joinpath('BIDS_VERSION').read_text().rstrip()
```

**Verification:**
```python
assert result['bids_version'] == expected_version
```

### Step 8: Assign selected_path = os.path.join(...)

```python
selected_path = os.path.join(root, f)
```

### Step 9: Call selected_paths.append()

```python
selected_paths.append(selected_path)
```


## Complete Example

```python
# Setup
# Fixtures: bids_examples, tmp_path

# Workflow
selected_dir = os.path.join(bids_examples, BIDS_SELECTION[0])
selected_paths = []
for root, dirs, files in os.walk(selected_dir, topdown=False):
    for f in files:
        selected_path = os.path.join(root, f)
        selected_paths.append(selected_path)
result = validate_bids(selected_paths, schema_path=False)
result = validate_bids(selected_paths, report_path=True)
result = validate_bids(selected_paths, report_path=os.path.join(tmp_path, 'test_bids.log'))
assert len(result['path_tracking']) == 0
schema_path = load.readable('schema')
expected_version = schema_path.joinpath('BIDS_VERSION').read_text().rstrip()
assert result['bids_version'] == expected_version
```

## Next Steps


---

*Source: test_validator.py:136 | Complexity: Advanced | Last updated: 2026-05-18*