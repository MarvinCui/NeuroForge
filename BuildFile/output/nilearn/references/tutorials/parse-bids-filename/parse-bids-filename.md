# How To: Parse Bids Filename

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check that a typical BIDS file is properly parsed.

## Prerequisites

**Required Modules:**
- `json`
- `pathlib`
- `pytest`
- `nilearn._utils.data_gen`
- `nilearn.interfaces.bids.query`


## Step-by-Step Guide

### Step 1: 'Check that a typical BIDS file is properly parsed.'

```python
'Check that a typical BIDS file is properly parsed.'
```

**Verification:**
```python
assert file_dict['extension'] == 'nii.gz'
```

### Step 2: Assign fields = value

```python
fields = ['sub', 'ses', 'task', 'lolo']
```

**Verification:**
```python
assert file_dict['suffix'] == 'bold'
```

### Step 3: Assign labels = value

```python
labels = ['01', '01', 'langloc+foo', 'lala']
```

**Verification:**
```python
assert file_dict['file_path'] == file_path
```

### Step 4: Assign file_name = 'sub-01_ses-01_task-langloc+foo_lolo-lala_bold.nii.gz'

```python
file_name = 'sub-01_ses-01_task-langloc+foo_lolo-lala_bold.nii.gz'
```

**Verification:**
```python
assert file_dict['file_basename'] == file_name
```

### Step 5: Assign file_path = Path(...)

```python
file_path = Path('dataset', 'sub-01', 'ses-01', 'func', file_name)
```

**Verification:**
```python
assert file_dict['entities'] == entities
```

### Step 6: Assign file_dict = parse_bids_filename(...)

```python
file_dict = parse_bids_filename(file_path)
```

**Verification:**
```python
assert file_dict['extension'] == 'nii.gz'
```

### Step 7: Assign entities = value

```python
entities = {field: labels[fidx] for fidx, field in enumerate(fields)}
```

**Verification:**
```python
assert file_dict['entities'] == entities
```


## Complete Example

```python
# Workflow
'Check that a typical BIDS file is properly parsed.'
fields = ['sub', 'ses', 'task', 'lolo']
labels = ['01', '01', 'langloc+foo', 'lala']
file_name = 'sub-01_ses-01_task-langloc+foo_lolo-lala_bold.nii.gz'
file_path = Path('dataset', 'sub-01', 'ses-01', 'func', file_name)
file_dict = parse_bids_filename(file_path)
assert file_dict['extension'] == 'nii.gz'
assert file_dict['suffix'] == 'bold'
assert file_dict['file_path'] == file_path
assert file_dict['file_basename'] == file_name
entities = {field: labels[fidx] for fidx, field in enumerate(fields)}
assert file_dict['entities'] == entities
```

## Next Steps


---

*Source: test_query.py:19 | Complexity: Intermediate | Last updated: 2026-05-18*