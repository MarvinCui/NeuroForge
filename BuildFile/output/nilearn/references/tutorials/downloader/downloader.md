# How To: Downloader

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test downloader

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
# Fixtures: tmp_path, request_mocker
```

## Step-by-Step Guide

### Step 1: Assign local_archive = value

```python
local_archive = Path(__file__).parent / 'data' / 'craddock_2011_parcellations.tar.gz'
```

**Verification:**
```python
assert stuff == 'stuff'
```

### Step 2: Assign url = 'http://example.com/craddock_atlas'

```python
url = 'http://example.com/craddock_atlas'
```

**Verification:**
```python
assert stuff == ''
```

### Step 3: Assign unknown = local_archive

```python
request_mocker.url_mapping['*craddock*'] = local_archive
```

### Step 4: Assign datasetdir = value

```python
datasetdir = tmp_path / 'craddock_2012'
```

### Step 5: Call datasetdir.mkdir()

```python
datasetdir.mkdir()
```

### Step 6: Assign dummy_file = value

```python
dummy_file = datasetdir / 'random_all.nii.gz'
```

### Step 7: Assign opts = value

```python
opts = {'uncompress': True}
```

### Step 8: Assign files = value

```python
files = [('random_all.nii.gz', url, opts), ('bald.nii.gz', url, opts)]
```

**Verification:**
```python
assert stuff == 'stuff'
```

### Step 9: Call fetch_atlas_craddock_2012()

```python
fetch_atlas_craddock_2012(data_dir=tmp_path)
```

**Verification:**
```python
assert stuff == ''
```

### Step 10: Call f.write()

```python
f.write('stuff')
```

### Step 11: Call fetch_files()

```python
fetch_files(str(tmp_path / 'craddock_2012'), files, verbose=0)
```

### Step 12: Assign stuff = f.read(...)

```python
stuff = f.read(5)
```

### Step 13: Assign stuff = f.read(...)

```python
stuff = f.read()
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, request_mocker

# Workflow
local_archive = Path(__file__).parent / 'data' / 'craddock_2011_parcellations.tar.gz'
url = 'http://example.com/craddock_atlas'
request_mocker.url_mapping['*craddock*'] = local_archive
datasetdir = tmp_path / 'craddock_2012'
datasetdir.mkdir()
dummy_file = datasetdir / 'random_all.nii.gz'
with dummy_file.open('w') as f:
    f.write('stuff')
opts = {'uncompress': True}
files = [('random_all.nii.gz', url, opts), ('bald.nii.gz', url, opts)]
with pytest.raises(IOError):
    fetch_files(str(tmp_path / 'craddock_2012'), files, verbose=0)
with dummy_file.open('r') as f:
    stuff = f.read(5)
assert stuff == 'stuff'
fetch_atlas_craddock_2012(data_dir=tmp_path)
with dummy_file.open() as f:
    stuff = f.read()
assert stuff == ''
```

## Next Steps


---

*Source: test_atlas.py:69 | Complexity: Advanced | Last updated: 2026-05-18*