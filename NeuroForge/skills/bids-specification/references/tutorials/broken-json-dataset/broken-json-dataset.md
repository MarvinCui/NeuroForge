# How To: Broken Json Dataset

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Perhaps this can be integrated into
https://github.com/bids-standard/bids-error-examples .

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

### Step 1: 'Perhaps this can be integrated into\n    https://github.com/bids-standard/bids-error-examples .'

```python
'Perhaps this can be integrated into\n    https://github.com/bids-standard/bids-error-examples .'
```

### Step 2: Assign dataset = 'asl003'

```python
dataset = 'asl003'
```

### Step 3: Assign dataset_path = os.path.join(...)

```python
dataset_path = os.path.join(bids_examples, dataset)
```

### Step 4: Assign dataset_json = os.path.join(...)

```python
dataset_json = os.path.join(dataset_path, 'dataset_description.json')
```

### Step 5: Assign broken_json = load_test_data(...)

```python
broken_json = load_test_data('broken_dataset_description.json')
```

### Step 6: Call shutil.copyfile()

```python
shutil.copyfile(broken_json, dataset_json)
```

### Step 7: Assign _ = validate_bids(...)

```python
_ = validate_bids(dataset_path, report_path=True)
```


## Complete Example

```python
# Setup
# Fixtures: bids_examples, tmp_path

# Workflow
'Perhaps this can be integrated into\n    https://github.com/bids-standard/bids-error-examples .'
dataset = 'asl003'
dataset_path = os.path.join(bids_examples, dataset)
dataset_json = os.path.join(dataset_path, 'dataset_description.json')
broken_json = load_test_data('broken_dataset_description.json')
shutil.copyfile(broken_json, dataset_json)
_ = validate_bids(dataset_path, report_path=True)
```

## Next Steps


---

*Source: test_validator.py:167 | Complexity: Intermediate | Last updated: 2026-05-18*