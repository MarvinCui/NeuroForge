# How To: Fetch Atlas Aal

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, mock, workflow, integration

## Overview

Workflow: test fetch atlas aal

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
# Fixtures: version, archive_format, url_key, aal_archive_root, tmp_path, request_mocker, img_3d_rand_eye
```

## Step-by-Step Guide

### Step 1: Assign metadata = '1\t2\t3\n'

```python
metadata = '1\t2\t3\n'
```

**Verification:**
```python
assert isinstance(dataset.maps, str)
```

### Step 2: Assign label_file = value

```python
label_file = 'AAL.xml' if version == 'SPM12' else 'ROI_MNI_V4.txt'
```

**Verification:**
```python
assert isinstance(dataset.indices, list)
```

### Step 3: Assign atlas_file = value

```python
atlas_file = 'AAL.nii' if version == 'SPM12' else 'ROI_MNI_V4.nii'
```

**Verification:**
```python
assert request_mocker.url_count == 1
```

### Step 4: Assign mock_file = value

```python
mock_file = tmp_path / f'aal_{version}' / aal_archive_root / atlas_file
```

### Step 5: Call mock_file.parent.mkdir()

```python
mock_file.parent.mkdir(exist_ok=True, parents=True)
```

### Step 6: Call img_3d_rand_eye.to_filename()

```python
img_3d_rand_eye.to_filename(mock_file)
```

### Step 7: Assign aal_data = dict_to_archive(...)

```python
aal_data = dict_to_archive({aal_archive_root / label_file: metadata, aal_archive_root / atlas_file: mock_file}, archive_format=archive_format)
```

### Step 8: Assign unknown = aal_data

```python
request_mocker.url_mapping[f'*{url_key}*'] = aal_data
```

### Step 9: Assign dataset = fetch_atlas_aal(...)

```python
dataset = fetch_atlas_aal(version=version, data_dir=tmp_path, verbose=0)
```

### Step 10: Call validate_atlas()

```python
validate_atlas(dataset)
```

**Verification:**
```python
assert isinstance(dataset.maps, str)
```

### Step 11: Assign metadata = b"<?xml version='1.0' encoding='us-ascii'?><metadata><label><index>1</index><name>A</name></label></metadata>"

```python
metadata = b"<?xml version='1.0' encoding='us-ascii'?><metadata><label><index>1</index><name>A</name></label></metadata>"
```


## Complete Example

```python
# Setup
# Fixtures: version, archive_format, url_key, aal_archive_root, tmp_path, request_mocker, img_3d_rand_eye

# Workflow
metadata = '1\t2\t3\n'
if version == 'SPM12':
    metadata = b"<?xml version='1.0' encoding='us-ascii'?><metadata><label><index>1</index><name>A</name></label></metadata>"
label_file = 'AAL.xml' if version == 'SPM12' else 'ROI_MNI_V4.txt'
atlas_file = 'AAL.nii' if version == 'SPM12' else 'ROI_MNI_V4.nii'
mock_file = tmp_path / f'aal_{version}' / aal_archive_root / atlas_file
mock_file.parent.mkdir(exist_ok=True, parents=True)
img_3d_rand_eye.to_filename(mock_file)
aal_data = dict_to_archive({aal_archive_root / label_file: metadata, aal_archive_root / atlas_file: mock_file}, archive_format=archive_format)
request_mocker.url_mapping[f'*{url_key}*'] = aal_data
dataset = fetch_atlas_aal(version=version, data_dir=tmp_path, verbose=0)
validate_atlas(dataset)
assert isinstance(dataset.maps, str)
assert isinstance(dataset.indices, list)
assert request_mocker.url_count == 1
```

## Next Steps


---

*Source: test_atlas.py:558 | Complexity: Advanced | Last updated: 2026-05-18*