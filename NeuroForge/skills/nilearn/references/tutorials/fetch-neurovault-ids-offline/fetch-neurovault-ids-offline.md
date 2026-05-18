# How To: Fetch Neurovault Ids Offline

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check image can be loaded again from disk.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `hashlib`
- `json`
- `os`
- `re`
- `stat`
- `pathlib`
- `urllib`
- `numpy`
- `pandas`
- `pytest`
- `requests`
- `nilearn._utils.data_gen`
- `nilearn.conftest`
- `nilearn.datasets`
- `nilearn.image`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Check image can be loaded again from disk.'

```python
'Check image can be loaded again from disk.'
```

**Verification:**
```python
assert len(data.images) == 1
```

### Step 2: Assign unknown = _get_neurovault_data(...)

```python
collections, images = _get_neurovault_data()
```

### Step 3: Assign collections = collections.sort_values(...)

```python
collections = collections.sort_values(by='true_number_of_images', ascending=False)
```

### Step 4: Assign unknown = value

```python
other_col_id, *col_ids = collections['id'].to_numpy()[:3]
```

### Step 5: Assign img_ids = value

```python
img_ids = images[images['collection_id'] == other_col_id]['id'].to_numpy()[:3]
```

### Step 6: Assign data = fetch_neurovault_ids(...)

```python
data = fetch_neurovault_ids(image_ids=img_ids, collection_ids=col_ids, data_dir=tmp_path)
```

### Step 7: Assign data = fetch_neurovault_ids(...)

```python
data = fetch_neurovault_ids(image_ids=[img_ids[0]], data_dir=tmp_path, mode='offline')
```

**Verification:**
```python
assert len(data.images) == 1
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Check image can be loaded again from disk.'
collections, images = _get_neurovault_data()
collections = collections.sort_values(by='true_number_of_images', ascending=False)
other_col_id, *col_ids = collections['id'].to_numpy()[:3]
img_ids = images[images['collection_id'] == other_col_id]['id'].to_numpy()[:3]
data = fetch_neurovault_ids(image_ids=img_ids, collection_ids=col_ids, data_dir=tmp_path)
data = fetch_neurovault_ids(image_ids=[img_ids[0]], data_dir=tmp_path, mode='offline')
assert len(data.images) == 1
```

## Next Steps


---

*Source: test_neurovault.py:879 | Complexity: Intermediate | Last updated: 2026-05-18*