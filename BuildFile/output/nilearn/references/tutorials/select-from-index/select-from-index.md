# How To: Select From Index

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test select from index

## Prerequisites

**Required Modules:**
- `json`
- `re`
- `shutil`
- `tempfile`
- `uuid`
- `collections`
- `pathlib`
- `numpy`
- `pandas`
- `pytest`
- `nibabel`
- `sklearn.utils`
- `nilearn._utils.data_gen`
- `nilearn._utils.helpers`
- `nilearn.datasets`
- `nilearn.datasets._utils`
- `nilearn.datasets.tests._testing`
- `nilearn.image`


## Step-by-Step Guide

### Step 1: Assign dataset_version = 'ds000030_R1.0.4'

```python
dataset_version = 'ds000030_R1.0.4'
```

**Verification:**
```python
assert len(new_urls) == 6
```

### Step 2: Assign data_prefix = value

```python
data_prefix = f"{dataset_version.split('_')[0]}/{dataset_version}/uncompressed"
```

**Verification:**
```python
assert data_prefix + '/sub-yyy.html' not in new_urls
```

### Step 3: Assign urls = value

```python
urls = [f'{data_prefix}/{f}' for f in ['stuff.html', 'sub-xxx.html', 'sub-yyy.html', 'sub-xxx/ses-01_task-rest.txt', 'sub-xxx/ses-01_task-other.txt', 'sub-xxx/ses-02_task-rest.txt', 'sub-xxx/ses-02_task-other.txt', 'sub-yyy/ses-01.txt', 'sub-yyy/ses-02.txt']]
```

**Verification:**
```python
assert len(new_urls) == 9
```

### Step 4: Assign new_urls = func.select_from_index(...)

```python
new_urls = func.select_from_index(urls, n_subjects=1)
```

**Verification:**
```python
assert data_prefix + '/sub-yyy.html' in new_urls
```

### Step 5: Assign new_urls = func.select_from_index(...)

```python
new_urls = func.select_from_index(urls, n_subjects=2)
```

**Verification:**
```python
assert len(new_urls) == 9
```

### Step 6: Assign new_urls = func.select_from_index(...)

```python
new_urls = func.select_from_index(urls, n_subjects=None)
```

**Verification:**
```python
assert len(new_urls) == 2
```

### Step 7: Assign new_urls = func.select_from_index(...)

```python
new_urls = func.select_from_index(urls, inclusion_filters=['*task-rest*'])
```

**Verification:**
```python
assert data_prefix + '/stuff.html' not in new_urls
```

### Step 8: Assign new_urls = func.select_from_index(...)

```python
new_urls = func.select_from_index(urls, exclusion_filters=['*ses-01*'])
```

**Verification:**
```python
assert len(new_urls) == 6
```

### Step 9: Assign new_urls = func.select_from_index(...)

```python
new_urls = func.select_from_index(urls, inclusion_filters=['*task-rest*'], exclusion_filters=['*ses-01*'])
```

**Verification:**
```python
assert data_prefix + '/stuff.html' in new_urls
```


## Complete Example

```python
# Workflow
dataset_version = 'ds000030_R1.0.4'
data_prefix = f"{dataset_version.split('_')[0]}/{dataset_version}/uncompressed"
urls = [f'{data_prefix}/{f}' for f in ['stuff.html', 'sub-xxx.html', 'sub-yyy.html', 'sub-xxx/ses-01_task-rest.txt', 'sub-xxx/ses-01_task-other.txt', 'sub-xxx/ses-02_task-rest.txt', 'sub-xxx/ses-02_task-other.txt', 'sub-yyy/ses-01.txt', 'sub-yyy/ses-02.txt']]
new_urls = func.select_from_index(urls, n_subjects=1)
assert len(new_urls) == 6
assert data_prefix + '/sub-yyy.html' not in new_urls
new_urls = func.select_from_index(urls, n_subjects=2)
assert len(new_urls) == 9
assert data_prefix + '/sub-yyy.html' in new_urls
new_urls = func.select_from_index(urls, n_subjects=None)
assert len(new_urls) == 9
new_urls = func.select_from_index(urls, inclusion_filters=['*task-rest*'])
assert len(new_urls) == 2
assert data_prefix + '/stuff.html' not in new_urls
new_urls = func.select_from_index(urls, exclusion_filters=['*ses-01*'])
assert len(new_urls) == 6
assert data_prefix + '/stuff.html' in new_urls
new_urls = func.select_from_index(urls, inclusion_filters=['*task-rest*'], exclusion_filters=['*ses-01*'])
assert len(new_urls) == 1
assert data_prefix + '/sub-xxx/ses-02_task-rest.txt' in new_urls
```

## Next Steps


---

*Source: test_func.py:832 | Complexity: Advanced | Last updated: 2026-05-18*