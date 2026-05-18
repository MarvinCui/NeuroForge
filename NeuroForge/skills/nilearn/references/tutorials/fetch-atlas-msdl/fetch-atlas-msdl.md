# How To: Fetch Atlas Msdl

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test fetch atlas msdl

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `itertools`
- `re`
- `xml.etree.ElementTree`
- `pathlib`
- `numpy`
- `pandas`
- `pytest`
- `nibabel`
- `numpy.testing`
- `sklearn.utils`
- `nilearn._utils`
- `nilearn._utils.testing`
- `nilearn.conftest`
- `nilearn.datasets`
- `nilearn.datasets._utils`
- `nilearn.datasets.atlas`
- `nilearn.datasets.tests._testing`
- `nilearn.image`

**Setup Required:**
```python
# Fixtures: tmp_path, request_mocker, capsys
```

## Step-by-Step Guide

### Step 1: Assign labels = pd.DataFrame(...)

```python
labels = pd.DataFrame({'x': [1.5, 1.2], 'y': [1.5, 1.3], 'z': [1.5, 1.4], 'name': ['Aud', 'DMN'], 'net name': ['Aud', 'DMN']})
```

**Verification:**
```python
assert isinstance(dataset.region_coords, list)
```

### Step 2: Assign root = Path(...)

```python
root = Path('MSDL_rois')
```

**Verification:**
```python
assert isinstance(dataset.networks, list)
```

### Step 3: Assign archive = value

```python
archive = {root / 'msdl_rois_labels.csv': labels.to_csv(index=False), root / 'msdl_rois.nii': '', root / 'README.txt': ''}
```

**Verification:**
```python
assert isinstance(dataset.maps, str)
```

### Step 4: Assign unknown = dict_to_archive(...)

```python
request_mocker.url_mapping['*MSDL_rois.zip'] = dict_to_archive(archive, 'zip')
```

**Verification:**
```python
assert request_mocker.url_count == 1
```

### Step 5: Assign dataset = fetch_atlas_msdl(...)

```python
dataset = fetch_atlas_msdl(data_dir=tmp_path, verbose=0)
```

### Step 6: Call validate_atlas()

```python
validate_atlas(dataset)
```

**Verification:**
```python
assert isinstance(dataset.region_coords, list)
```

### Step 7: Call check_fetcher_verbosity()

```python
check_fetcher_verbosity(fetch_atlas_msdl, capsys, data_dir=tmp_path)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, request_mocker, capsys

# Workflow
labels = pd.DataFrame({'x': [1.5, 1.2], 'y': [1.5, 1.3], 'z': [1.5, 1.4], 'name': ['Aud', 'DMN'], 'net name': ['Aud', 'DMN']})
root = Path('MSDL_rois')
archive = {root / 'msdl_rois_labels.csv': labels.to_csv(index=False), root / 'msdl_rois.nii': '', root / 'README.txt': ''}
request_mocker.url_mapping['*MSDL_rois.zip'] = dict_to_archive(archive, 'zip')
dataset = fetch_atlas_msdl(data_dir=tmp_path, verbose=0)
validate_atlas(dataset)
assert isinstance(dataset.region_coords, list)
assert isinstance(dataset.networks, list)
assert isinstance(dataset.maps, str)
assert request_mocker.url_count == 1
check_fetcher_verbosity(fetch_atlas_msdl, capsys, data_dir=tmp_path)
```

## Next Steps


---

*Source: test_atlas.py:388 | Complexity: Intermediate | Last updated: 2026-05-18*