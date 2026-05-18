# How To: Fetch Atlas Schaefer 2018

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, mock, workflow, integration

## Overview

Workflow: test fetch atlas schaefer 2018

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
# Fixtures: tmp_path, request_mocker, n_rois, yeo_networks, resolution_mm, capsys
```

## Step-by-Step Guide

### Step 1: Assign labels_pattern = re.compile(...)

```python
labels_pattern = re.compile('.*2018_(?P<n_rois>\\d+)Parcels_(?P<network>\\d+)Networks_order.txt')
```

**Verification:**
```python
assert isinstance(data.maps, str)
```

### Step 2: Assign img_pattern = re.compile(...)

```python
img_pattern = re.compile('.*_(?P<n_rois>\\d+)Parcels_(?P<network>\\d+)Networks_order_FSLMNI152_(?P<res>\\d)mm.nii.gz')
```

**Verification:**
```python
assert len(data.labels) == n_rois
```

### Step 3: Assign unknown = _schaefer_labels

```python
request_mocker.url_mapping[labels_pattern] = _schaefer_labels
```

**Verification:**
```python
assert data.labels[0] == 'Background'
```

### Step 4: Assign unknown = _schaefer_img

```python
request_mocker.url_mapping[img_pattern] = _schaefer_img
```

**Verification:**
```python
assert data.labels[1].startswith(f'{yeo_networks}Networks')
```

### Step 5: Assign mock_lut = pd.DataFrame(...)

```python
mock_lut = pd.DataFrame({'name': [f'{yeo_networks}Networks_{x}' for x in range(1, n_rois)], 'r': [1] * (n_rois - 1), 'g': [1] * (n_rois - 1), 'b': [1] * (n_rois - 1), 'o': [0] * (n_rois - 1)})
```

**Verification:**
```python
assert img.header.get_zooms()[0] == resolution_mm
```

### Step 6: Assign basename = value

```python
basename = f'Schaefer2018_{n_rois}Parcels_{yeo_networks}Networks_order.txt'
```

**Verification:**
```python
assert np.array_equal(np.unique(img.dataobj), np.arange(n_rois + 1))
```

### Step 7: Assign mock_dir = value

```python
mock_dir = tmp_path / 'schaefer_2018'
```

### Step 8: Call mock_dir.mkdir()

```python
mock_dir.mkdir(exist_ok=True, parents=True)
```

### Step 9: Assign mock_file = value

```python
mock_file = mock_dir / basename
```

### Step 10: Call mock_lut.to_csv()

```python
mock_lut.to_csv(mock_file, sep='\t', header=False)
```

### Step 11: Assign data = fetch_atlas_schaefer_2018(...)

```python
data = fetch_atlas_schaefer_2018(n_rois=n_rois, yeo_networks=yeo_networks, resolution_mm=resolution_mm, data_dir=tmp_path, verbose=0)
```

### Step 12: Call validate_atlas()

```python
validate_atlas(data)
```

**Verification:**
```python
assert isinstance(data.maps, str)
```

### Step 13: Assign img = load(...)

```python
img = load(data.maps)
```

**Verification:**
```python
assert img.header.get_zooms()[0] == resolution_mm
```

### Step 14: Call check_fetcher_verbosity()

```python
check_fetcher_verbosity(fetch_atlas_schaefer_2018, capsys, n_rois=n_rois, yeo_networks=yeo_networks, resolution_mm=resolution_mm, data_dir=tmp_path)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, request_mocker, n_rois, yeo_networks, resolution_mm, capsys

# Workflow
labels_pattern = re.compile('.*2018_(?P<n_rois>\\d+)Parcels_(?P<network>\\d+)Networks_order.txt')
img_pattern = re.compile('.*_(?P<n_rois>\\d+)Parcels_(?P<network>\\d+)Networks_order_FSLMNI152_(?P<res>\\d)mm.nii.gz')
request_mocker.url_mapping[labels_pattern] = _schaefer_labels
request_mocker.url_mapping[img_pattern] = _schaefer_img
mock_lut = pd.DataFrame({'name': [f'{yeo_networks}Networks_{x}' for x in range(1, n_rois)], 'r': [1] * (n_rois - 1), 'g': [1] * (n_rois - 1), 'b': [1] * (n_rois - 1), 'o': [0] * (n_rois - 1)})
basename = f'Schaefer2018_{n_rois}Parcels_{yeo_networks}Networks_order.txt'
mock_dir = tmp_path / 'schaefer_2018'
mock_dir.mkdir(exist_ok=True, parents=True)
mock_file = mock_dir / basename
mock_lut.to_csv(mock_file, sep='\t', header=False)
data = fetch_atlas_schaefer_2018(n_rois=n_rois, yeo_networks=yeo_networks, resolution_mm=resolution_mm, data_dir=tmp_path, verbose=0)
validate_atlas(data)
assert isinstance(data.maps, str)
assert len(data.labels) == n_rois
assert data.labels[0] == 'Background'
assert data.labels[1].startswith(f'{yeo_networks}Networks')
img = load(data.maps)
assert img.header.get_zooms()[0] == resolution_mm
assert np.array_equal(np.unique(img.dataobj), np.arange(n_rois + 1))
check_fetcher_verbosity(fetch_atlas_schaefer_2018, capsys, n_rois=n_rois, yeo_networks=yeo_networks, resolution_mm=resolution_mm, data_dir=tmp_path)
```

## Next Steps


---

*Source: test_atlas.py:824 | Complexity: Advanced | Last updated: 2026-05-18*