# How To: Fetch Surf Fsaverage

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, mock, workflow, integration

## Overview

Workflow: test fetch surf fsaverage

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `pandas`
- `pytest`
- `nibabel`
- `sklearn.utils`
- `nilearn._utils.helpers`
- `nilearn.datasets.struct`
- `nilearn.datasets.tests._testing`
- `nilearn.surface`

**Setup Required:**
```python
# Fixtures: mesh, tmp_path, request_mocker
```

## Step-by-Step Guide

### Step 1: Assign mesh_attributes = value

```python
mesh_attributes = {f'{part}_{side}' for part in ['area', 'curv', 'flat', 'infl', 'pial', 'sphere', 'sulc', 'thick', 'white'] for side in ['left', 'right']}
```

**Verification:**
```python
assert mesh_attributes.issubset(set(dataset.keys()))
```

### Step 2: Assign fs_urls = value

```python
fs_urls = ['https://osf.io/azhdf/download', 'https://osf.io/28uma/download', 'https://osf.io/jzxyr/download', 'https://osf.io/svf8k/download']
```

### Step 3: Assign dataset = fetch_surf_fsaverage(...)

```python
dataset = fetch_surf_fsaverage(mesh, data_dir=str(tmp_path))
```

### Step 4: Call check_type_fetcher()

```python
check_type_fetcher(dataset)
```

**Verification:**
```python
assert mesh_attributes.issubset(set(dataset.keys()))
```

### Step 5: Assign unknown = list_to_archive(...)

```python
request_mocker.url_mapping[fs_url] = list_to_archive([f'{name}.gii.gz' for name in mesh_attributes])
```


## Complete Example

```python
# Setup
# Fixtures: mesh, tmp_path, request_mocker

# Workflow
mesh_attributes = {f'{part}_{side}' for part in ['area', 'curv', 'flat', 'infl', 'pial', 'sphere', 'sulc', 'thick', 'white'] for side in ['left', 'right']}
fs_urls = ['https://osf.io/azhdf/download', 'https://osf.io/28uma/download', 'https://osf.io/jzxyr/download', 'https://osf.io/svf8k/download']
for fs_url in fs_urls:
    request_mocker.url_mapping[fs_url] = list_to_archive([f'{name}.gii.gz' for name in mesh_attributes])
dataset = fetch_surf_fsaverage(mesh, data_dir=str(tmp_path))
check_type_fetcher(dataset)
assert mesh_attributes.issubset(set(dataset.keys()))
```

## Next Steps


---

*Source: test_struct.py:166 | Complexity: Intermediate | Last updated: 2026-05-18*