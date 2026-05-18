# How To: Fetch Atlas Basc Multiscale 2015

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test fetch atlas basc multiscale 2015

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
# Fixtures: tmp_path, capsys
```

## Step-by-Step Guide

### Step 1: Assign resolution = 7

```python
resolution = 7
```

**Verification:**
```python
assert data_sym['maps'] == str(tmp_path / dataset_name / name_sym / basename_sym)
```

### Step 2: Assign dataset_name = 'basc_multiscale_2015'

```python
dataset_name = 'basc_multiscale_2015'
```

**Verification:**
```python
assert data_asym['maps'] == str(tmp_path / dataset_name / name_asym / basename_asym)
```

### Step 3: Assign name_sym = 'template_cambridge_basc_multiscale_nii_sym'

```python
name_sym = 'template_cambridge_basc_multiscale_nii_sym'
```

### Step 4: Assign basename_sym = 'template_cambridge_basc_multiscale_sym_scale007.nii.gz'

```python
basename_sym = 'template_cambridge_basc_multiscale_sym_scale007.nii.gz'
```

### Step 5: Assign mock_map = data_gen.generate_labeled_regions(...)

```python
mock_map = data_gen.generate_labeled_regions((53, 64, 52), resolution)
```

### Step 6: Assign mock_file = value

```python
mock_file = tmp_path / dataset_name / name_sym / basename_sym
```

### Step 7: Call mock_file.parent.mkdir()

```python
mock_file.parent.mkdir(exist_ok=True, parents=True)
```

### Step 8: Call mock_map.to_filename()

```python
mock_map.to_filename(mock_file)
```

### Step 9: Assign data_sym = fetch_atlas_basc_multiscale_2015(...)

```python
data_sym = fetch_atlas_basc_multiscale_2015(data_dir=tmp_path, verbose=0, resolution=resolution)
```

### Step 10: Call validate_atlas()

```python
validate_atlas(data_sym)
```

**Verification:**
```python
assert data_sym['maps'] == str(tmp_path / dataset_name / name_sym / basename_sym)
```

### Step 11: Assign name_asym = 'template_cambridge_basc_multiscale_nii_asym'

```python
name_asym = 'template_cambridge_basc_multiscale_nii_asym'
```

### Step 12: Assign basename_asym = 'template_cambridge_basc_multiscale_asym_scale007.nii.gz'

```python
basename_asym = 'template_cambridge_basc_multiscale_asym_scale007.nii.gz'
```

### Step 13: Assign mock_file = value

```python
mock_file = tmp_path / dataset_name / name_asym / basename_asym
```

### Step 14: Call mock_file.parent.mkdir()

```python
mock_file.parent.mkdir(exist_ok=True, parents=True)
```

### Step 15: Call mock_map.to_filename()

```python
mock_map.to_filename(mock_file)
```

### Step 16: Assign data_asym = fetch_atlas_basc_multiscale_2015(...)

```python
data_asym = fetch_atlas_basc_multiscale_2015(version='asym', verbose=0, data_dir=tmp_path, resolution=resolution)
```

### Step 17: Call validate_atlas()

```python
validate_atlas(data_asym)
```

**Verification:**
```python
assert data_asym['maps'] == str(tmp_path / dataset_name / name_asym / basename_asym)
```

### Step 18: Call check_fetcher_verbosity()

```python
check_fetcher_verbosity(fetch_atlas_basc_multiscale_2015, capsys, data_dir=tmp_path)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, capsys

# Workflow
resolution = 7
dataset_name = 'basc_multiscale_2015'
name_sym = 'template_cambridge_basc_multiscale_nii_sym'
basename_sym = 'template_cambridge_basc_multiscale_sym_scale007.nii.gz'
mock_map = data_gen.generate_labeled_regions((53, 64, 52), resolution)
mock_file = tmp_path / dataset_name / name_sym / basename_sym
mock_file.parent.mkdir(exist_ok=True, parents=True)
mock_map.to_filename(mock_file)
data_sym = fetch_atlas_basc_multiscale_2015(data_dir=tmp_path, verbose=0, resolution=resolution)
validate_atlas(data_sym)
assert data_sym['maps'] == str(tmp_path / dataset_name / name_sym / basename_sym)
name_asym = 'template_cambridge_basc_multiscale_nii_asym'
basename_asym = 'template_cambridge_basc_multiscale_asym_scale007.nii.gz'
mock_file = tmp_path / dataset_name / name_asym / basename_asym
mock_file.parent.mkdir(exist_ok=True, parents=True)
mock_map.to_filename(mock_file)
data_asym = fetch_atlas_basc_multiscale_2015(version='asym', verbose=0, data_dir=tmp_path, resolution=resolution)
validate_atlas(data_asym)
assert data_asym['maps'] == str(tmp_path / dataset_name / name_asym / basename_asym)
check_fetcher_verbosity(fetch_atlas_basc_multiscale_2015, capsys, data_dir=tmp_path)
```

## Next Steps


---

*Source: test_atlas.py:604 | Complexity: Advanced | Last updated: 2026-05-18*