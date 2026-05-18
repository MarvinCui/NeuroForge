# How To: Fetch Openneuro Dataset

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test fetch openneuro dataset

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: Assign dataset_version = 'ds000030_R1.0.4'

```python
dataset_version = 'ds000030_R1.0.4'
```

**Verification:**
```python
assert isinstance(datadir, str)
```

### Step 2: Assign data_prefix = value

```python
data_prefix = f"{dataset_version.split('_')[0]}/{dataset_version}/uncompressed"
```

**Verification:**
```python
assert isinstance(dl_files, list)
```

### Step 3: Assign data_dir = get_dataset_dir(...)

```python
data_dir = get_dataset_dir(data_prefix, data_dir=tmp_path)
```

**Verification:**
```python
assert len(dl_files) == 9
```

### Step 4: Assign url_file = value

```python
url_file = data_dir / 'urls.json'
```

### Step 5: Assign urls = value

```python
urls = [f'https://example.com/{data_prefix}/stuff.html', f'https://example.com/{data_prefix}/sub-xxx.html', f'https://example.com/{data_prefix}/sub-yyy.html', f'https://example.com/{data_prefix}/sub-xxx/ses-01_task-rest.txt', f'https://example.com/{data_prefix}/sub-xxx/ses-01_task-other.txt', f'https://example.com/{data_prefix}/sub-xxx/ses-02_task-rest.txt', f'https://example.com/{data_prefix}/sub-xxx/ses-02_task-other.txt', f'https://example.com/{data_prefix}/sub-yyy/ses-01.txt', f'https://example.com/{data_prefix}/sub-yyy/ses-02.txt']
```

### Step 6: Assign unknown = func.fetch_openneuro_dataset(...)

```python
datadir, dl_files = func.fetch_openneuro_dataset(urls, tmp_path, dataset_version)
```

**Verification:**
```python
assert isinstance(datadir, str)
```

### Step 7: Call json.dump()

```python
json.dump(urls, f)
```

### Step 8: Assign unknown = func.fetch_openneuro_dataset(...)

```python
_, urls = func.fetch_openneuro_dataset(urls=None, data_dir=tmp_path, dataset_version='ds500_v2')
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
dataset_version = 'ds000030_R1.0.4'
data_prefix = f"{dataset_version.split('_')[0]}/{dataset_version}/uncompressed"
data_dir = get_dataset_dir(data_prefix, data_dir=tmp_path)
url_file = data_dir / 'urls.json'
urls = [f'https://example.com/{data_prefix}/stuff.html', f'https://example.com/{data_prefix}/sub-xxx.html', f'https://example.com/{data_prefix}/sub-yyy.html', f'https://example.com/{data_prefix}/sub-xxx/ses-01_task-rest.txt', f'https://example.com/{data_prefix}/sub-xxx/ses-01_task-other.txt', f'https://example.com/{data_prefix}/sub-xxx/ses-02_task-rest.txt', f'https://example.com/{data_prefix}/sub-xxx/ses-02_task-other.txt', f'https://example.com/{data_prefix}/sub-yyy/ses-01.txt', f'https://example.com/{data_prefix}/sub-yyy/ses-02.txt']
with url_file.open('w') as f:
    json.dump(urls, f)
datadir, dl_files = func.fetch_openneuro_dataset(urls, tmp_path, dataset_version)
assert isinstance(datadir, str)
assert isinstance(dl_files, list)
assert len(dl_files) == 9
with pytest.warns(UserWarning, match='Downloading "ds000030_R1.0.4".'):
    _, urls = func.fetch_openneuro_dataset(urls=None, data_dir=tmp_path, dataset_version='ds500_v2')
```

## Next Steps


---

*Source: test_func.py:912 | Complexity: Advanced | Last updated: 2026-05-18*