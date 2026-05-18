# How To: Fetch Atlas Yeo 2011

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: Check fetcher for the Yeo atlas.

Mocks data for each deterministic atlas and their look up tables.

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

### Step 1: 'Check fetcher for the Yeo atlas.\n\n    Mocks data for each deterministic atlas and their look up tables.\n    '

```python
'Check fetcher for the Yeo atlas.\n\n    Mocks data for each deterministic atlas and their look up tables.\n    '
```

### Step 2: Assign yeo_data = _generate_yeo_data(...)

```python
yeo_data = _generate_yeo_data(tmp_path)
```

### Step 3: Assign unknown = yeo_data

```python
request_mocker.url_mapping['*Yeo_JNeurophysiol11_MNI152*'] = yeo_data
```

### Step 4: Assign dataset = fetch_atlas_yeo_2011(...)

```python
dataset = fetch_atlas_yeo_2011(data_dir=tmp_path, verbose=0)
```

### Step 5: Assign dataset = fetch_atlas_yeo_2011(...)

```python
dataset = fetch_atlas_yeo_2011(data_dir=tmp_path, verbose=0, n_networks=17)
```

### Step 6: Assign dataset = fetch_atlas_yeo_2011(...)

```python
dataset = fetch_atlas_yeo_2011(data_dir=tmp_path, verbose=0, thickness='thin')
```

### Step 7: Call validate_atlas()

```python
validate_atlas(dataset)
```

### Step 8: Call check_fetcher_verbosity()

```python
check_fetcher_verbosity(fetch_atlas_yeo_2011, capsys, data_dir=tmp_path)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, request_mocker, capsys

# Workflow
'Check fetcher for the Yeo atlas.\n\n    Mocks data for each deterministic atlas and their look up tables.\n    '
yeo_data = _generate_yeo_data(tmp_path)
request_mocker.url_mapping['*Yeo_JNeurophysiol11_MNI152*'] = yeo_data
dataset = fetch_atlas_yeo_2011(data_dir=tmp_path, verbose=0)
dataset = fetch_atlas_yeo_2011(data_dir=tmp_path, verbose=0, n_networks=17)
dataset = fetch_atlas_yeo_2011(data_dir=tmp_path, verbose=0, thickness='thin')
validate_atlas(dataset)
check_fetcher_verbosity(fetch_atlas_yeo_2011, capsys, data_dir=tmp_path)
```

## Next Steps


---

*Source: test_atlas.py:466 | Complexity: Advanced | Last updated: 2026-05-18*