# How To: Fetch Atlas Difumo

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test fetch atlas difumo

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

### Step 1: Assign resolutions = value

```python
resolutions = [2, 3]
```

**Verification:**
```python
assert len(dataset.labels) == dim
```

### Step 2: Assign dimensions = value

```python
dimensions = [64, 128, 256, 512, 1024]
```

**Verification:**
```python
assert isinstance(dataset.maps, str)
```

### Step 3: Assign dimension_urls = value

```python
dimension_urls = ['pqu9r', 'wjvd5', '3vrct', '9b76y', '34792']
```

**Verification:**
```python
assert request_mocker.url_count == url_count
```

### Step 4: Assign url_mapping = dict(...)

```python
url_mapping = dict(zip(dimensions, dimension_urls, strict=False))
```

### Step 5: Call check_fetcher_verbosity()

```python
check_fetcher_verbosity(fetch_atlas_difumo, capsys, data_dir=tmp_path)
```

### Step 6: Assign url = value

```python
url = f'*osf.io/{url_mapping[dim]}/*'
```

### Step 7: Assign labels = pd.DataFrame(...)

```python
labels = pd.DataFrame({'Component': list(range(1, dim + 1)), 'Difumo_names': ['' for _ in range(dim)], 'Yeo_networks7': ['' for _ in range(dim)], 'Yeo_networks17': ['' for _ in range(dim)], 'GM': ['' for _ in range(dim)], 'WM': ['' for _ in range(dim)], 'CSF': ['' for _ in range(dim)]})
```

### Step 8: Assign root = Path(...)

```python
root = Path(f'{dim}')
```

### Step 9: Assign archive = value

```python
archive = {root / f'labels_{dim}_dictionary.csv': labels.to_csv(index=False), root / '2mm' / 'maps.nii.gz': '', root / '3mm' / 'maps.nii.gz': ''}
```

### Step 10: Assign unknown = dict_to_archive(...)

```python
request_mocker.url_mapping[url] = dict_to_archive(archive, 'zip')
```

### Step 11: Call fetch_atlas_difumo()

```python
fetch_atlas_difumo(data_dir=tmp_path, dimension=42, resolution_mm=3)
```

### Step 12: Call fetch_atlas_difumo()

```python
fetch_atlas_difumo(data_dir=tmp_path, dimension=128, resolution_mm=3.14)
```

### Step 13: Assign dataset = fetch_atlas_difumo(...)

```python
dataset = fetch_atlas_difumo(data_dir=tmp_path, dimension=dim, resolution_mm=res, verbose=0)
```

### Step 14: Call validate_atlas()

```python
validate_atlas(dataset)
```

**Verification:**
```python
assert len(dataset.labels) == dim
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, request_mocker, capsys

# Workflow
resolutions = [2, 3]
dimensions = [64, 128, 256, 512, 1024]
dimension_urls = ['pqu9r', 'wjvd5', '3vrct', '9b76y', '34792']
url_mapping = dict(zip(dimensions, dimension_urls, strict=False))
for url_count, dim in enumerate(dimensions, start=2):
    url = f'*osf.io/{url_mapping[dim]}/*'
    labels = pd.DataFrame({'Component': list(range(1, dim + 1)), 'Difumo_names': ['' for _ in range(dim)], 'Yeo_networks7': ['' for _ in range(dim)], 'Yeo_networks17': ['' for _ in range(dim)], 'GM': ['' for _ in range(dim)], 'WM': ['' for _ in range(dim)], 'CSF': ['' for _ in range(dim)]})
    root = Path(f'{dim}')
    archive = {root / f'labels_{dim}_dictionary.csv': labels.to_csv(index=False), root / '2mm' / 'maps.nii.gz': '', root / '3mm' / 'maps.nii.gz': ''}
    request_mocker.url_mapping[url] = dict_to_archive(archive, 'zip')
    for res in resolutions:
        dataset = fetch_atlas_difumo(data_dir=tmp_path, dimension=dim, resolution_mm=res, verbose=0)
        validate_atlas(dataset)
        assert len(dataset.labels) == dim
        assert isinstance(dataset.maps, str)
        assert request_mocker.url_count == url_count
with pytest.raises(ValueError):
    fetch_atlas_difumo(data_dir=tmp_path, dimension=42, resolution_mm=3)
    fetch_atlas_difumo(data_dir=tmp_path, dimension=128, resolution_mm=3.14)
check_fetcher_verbosity(fetch_atlas_difumo, capsys, data_dir=tmp_path)
```

## Next Steps


---

*Source: test_atlas.py:497 | Complexity: Advanced | Last updated: 2026-05-18*