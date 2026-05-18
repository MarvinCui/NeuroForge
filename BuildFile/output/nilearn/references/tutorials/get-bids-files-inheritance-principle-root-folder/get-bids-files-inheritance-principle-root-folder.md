# How To: Get Bids Files Inheritance Principle Root Folder

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check if json files are found in root folder of a dataset.

see https://bids-specification.readthedocs.io/en/latest/common-principles.html#the-inheritance-principle

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

### Step 1: 'Check if json files are found in root folder of a dataset.\n\n    see https://bids-specification.readthedocs.io/en/latest/common-principles.html#the-inheritance-principle\n    '

```python
'Check if json files are found in root folder of a dataset.\n\n    see https://bids-specification.readthedocs.io/en/latest/common-principles.html#the-inheritance-principle\n    '
```

**Verification:**
```python
assert json_file.exists()
```

### Step 2: Assign bids_path = create_fake_bids_dataset(...)

```python
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=1, n_ses=1, tasks=['main'], n_runs=[1])
```

**Verification:**
```python
assert selection == []
```

### Step 3: Call _rm_all_json_files_from_bids_dataset()

```python
_rm_all_json_files_from_bids_dataset(bids_path)
```

**Verification:**
```python
assert selection != []
```

### Step 4: Assign json_file = 'task-main_bold.json'

```python
json_file = 'task-main_bold.json'
```

**Verification:**
```python
assert selection[0] == str(json_file)
```

### Step 5: Assign json_file = add_metadata_to_bids_dataset(...)

```python
json_file = add_metadata_to_bids_dataset(bids_path=bids_path, metadata={'RepetitionTime': 1.5}, json_file=json_file)
```

**Verification:**
```python
assert json_file.exists()
```

### Step 6: Assign selection = get_bids_files(...)

```python
selection = get_bids_files(bids_path, file_tag='bold', file_type='json', filters=[('task', 'main')], sub_folder=True)
```

**Verification:**
```python
assert selection == []
```

### Step 7: Assign selection = get_bids_files(...)

```python
selection = get_bids_files(bids_path, file_tag='bold', file_type='json', filters=[('task', 'main')], sub_folder=False)
```

**Verification:**
```python
assert selection != []
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Check if json files are found in root folder of a dataset.\n\n    see https://bids-specification.readthedocs.io/en/latest/common-principles.html#the-inheritance-principle\n    '
bids_path = create_fake_bids_dataset(base_dir=tmp_path, n_sub=1, n_ses=1, tasks=['main'], n_runs=[1])
_rm_all_json_files_from_bids_dataset(bids_path)
json_file = 'task-main_bold.json'
json_file = add_metadata_to_bids_dataset(bids_path=bids_path, metadata={'RepetitionTime': 1.5}, json_file=json_file)
assert json_file.exists()
selection = get_bids_files(bids_path, file_tag='bold', file_type='json', filters=[('task', 'main')], sub_folder=True)
assert selection == []
selection = get_bids_files(bids_path, file_tag='bold', file_type='json', filters=[('task', 'main')], sub_folder=False)
assert selection != []
assert selection[0] == str(json_file)
```

## Next Steps


---

*Source: test_query.py:147 | Complexity: Intermediate | Last updated: 2026-05-18*