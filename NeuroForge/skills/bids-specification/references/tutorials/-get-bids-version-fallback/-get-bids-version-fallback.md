# How To:  Get Bids Version Fallback

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test  get bids version fallback

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `json`
- `os`
- `subprocess`
- `collections.abc`
- `pytest`
- `jsonschema.exceptions`
- `bidsschematools`
- `data`
- `re`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: Assign expected_version = '1.2.3-dev'

```python
expected_version = '1.2.3-dev'
```

**Verification:**
```python
assert bids_version == expected_version
```

### Step 2: Assign schema_path = os.path.join(...)

```python
schema_path = os.path.join(tmp_path, 'whatever', expected_version)
```

**Verification:**
```python
assert bids_version == schema_path
```

### Step 3: Assign bids_version = schema._get_bids_version(...)

```python
bids_version = schema._get_bids_version(schema_path)
```

**Verification:**
```python
assert bids_version == expected_version
```

### Step 4: Assign schema_path = os.path.join(...)

```python
schema_path = os.path.join(tmp_path, 'whatever', 'undocumented_schema_dir')
```

### Step 5: Assign bids_version = schema._get_bids_version(...)

```python
bids_version = schema._get_bids_version(schema_path)
```

**Verification:**
```python
assert bids_version == schema_path
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
expected_version = '1.2.3-dev'
schema_path = os.path.join(tmp_path, 'whatever', expected_version)
bids_version = schema._get_bids_version(schema_path)
assert bids_version == expected_version
schema_path = os.path.join(tmp_path, 'whatever', 'undocumented_schema_dir')
bids_version = schema._get_bids_version(schema_path)
assert bids_version == schema_path
```

## Next Steps


---

*Source: test_schema.py:22 | Complexity: Intermediate | Last updated: 2026-05-18*