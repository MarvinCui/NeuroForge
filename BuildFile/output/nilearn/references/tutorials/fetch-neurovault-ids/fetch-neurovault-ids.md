# How To: Fetch Neurovault Ids

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test fetch_neurovault_ids.

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

### Step 1: 'Test fetch_neurovault_ids.'

```python
'Test fetch_neurovault_ids.'
```

**Verification:**
```python
assert len(data.images) == len(expected_images)
```

### Step 2: Assign unknown = _get_neurovault_data(...)

```python
collections, images = _get_neurovault_data()
```

**Verification:**
```python
assert {img['id'] for img in data['images_meta']} == set(expected_images)
```

### Step 3: Assign collections = collections.sort_values(...)

```python
collections = collections.sort_values(by='true_number_of_images', ascending=False)
```

**Verification:**
```python
assert Path(data['images'][0]).parent == Path(data['collections_meta'][0]['absolute_path'])
```

### Step 4: Assign unknown = value

```python
other_col_id, *col_ids = collections['id'].to_numpy()[:3]
```

**Verification:**
```python
assert isinstance(image, str)
```

### Step 5: Assign img_ids = value

```python
img_ids = images[images['collection_id'] == other_col_id]['id'].to_numpy()[:3]
```

**Verification:**
```python
assert not isinstance(value, Path)
```

### Step 6: Assign img_from_cols_ids = unknown.to_numpy(...)

```python
img_from_cols_ids = images[images['collection_id'].isin(col_ids)]['id'].to_numpy()
```

### Step 7: Assign data = fetch_neurovault_ids(...)

```python
data = fetch_neurovault_ids(image_ids=img_ids, collection_ids=col_ids, data_dir=tmp_path)
```

### Step 8: Assign expected_images = value

```python
expected_images = list(img_ids) + list(img_from_cols_ids)
```

**Verification:**
```python
assert len(data.images) == len(expected_images)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test fetch_neurovault_ids.'
collections, images = _get_neurovault_data()
collections = collections.sort_values(by='true_number_of_images', ascending=False)
other_col_id, *col_ids = collections['id'].to_numpy()[:3]
img_ids = images[images['collection_id'] == other_col_id]['id'].to_numpy()[:3]
img_from_cols_ids = images[images['collection_id'].isin(col_ids)]['id'].to_numpy()
data = fetch_neurovault_ids(image_ids=img_ids, collection_ids=col_ids, data_dir=tmp_path)
expected_images = list(img_ids) + list(img_from_cols_ids)
assert len(data.images) == len(expected_images)
assert {img['id'] for img in data['images_meta']} == set(expected_images)
assert Path(data['images'][0]).parent == Path(data['collections_meta'][0]['absolute_path'])
for image in data.images:
    assert isinstance(image, str)
for meta in data.images_meta + data.collections_meta:
    for value in meta.values():
        assert not isinstance(value, Path)
```

## Next Steps


---

*Source: test_neurovault.py:839 | Complexity: Advanced | Last updated: 2026-05-18*