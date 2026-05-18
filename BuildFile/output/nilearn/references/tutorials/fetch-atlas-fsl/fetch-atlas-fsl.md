# How To: Fetch Atlas Fsl

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test fetch atlas fsl

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
# Fixtures: name, label_fname, fname, is_symm, split, atlas_data, fsl_fetcher, tmp_path, affine_eye
```

## Step-by-Step Guide

### Step 1: Assign atlas_dir = value

```python
atlas_dir = tmp_path / 'fsl' / 'data' / 'atlases'
```

**Verification:**
```python
assert label.strip() == label
```

### Step 2: Assign nifti_dir = value

```python
nifti_dir = atlas_dir / name
```

### Step 3: Call nifti_dir.mkdir()

```python
nifti_dir.mkdir(parents=True)
```

### Step 4: Call _write_sample_atlas_metadata()

```python
_write_sample_atlas_metadata(atlas_dir, f'{name}{label_fname}', is_symm=is_symm)
```

### Step 5: Assign target_atlas_nii = value

```python
target_atlas_nii = nifti_dir / f'{name}-{fname}.nii.gz'
```

### Step 6: Call Nifti1Image.to_filename()

```python
Nifti1Image(atlas_data, affine_eye * 3).to_filename(target_atlas_nii)
```

### Step 7: Assign atlas_instance = fsl_fetcher(...)

```python
atlas_instance = fsl_fetcher(fname, data_dir=tmp_path, symmetric_split=split)
```

### Step 8: Call validate_atlas()

```python
validate_atlas(atlas_instance)
```

### Step 9: Call _test_atlas_instance_should_match_data()

```python
_test_atlas_instance_should_match_data(atlas_instance, is_symm=is_symm or split)
```

**Verification:**
```python
assert label.strip() == label
```


## Complete Example

```python
# Setup
# Fixtures: name, label_fname, fname, is_symm, split, atlas_data, fsl_fetcher, tmp_path, affine_eye

# Workflow
atlas_dir = tmp_path / 'fsl' / 'data' / 'atlases'
nifti_dir = atlas_dir / name
nifti_dir.mkdir(parents=True)
_write_sample_atlas_metadata(atlas_dir, f'{name}{label_fname}', is_symm=is_symm)
target_atlas_nii = nifti_dir / f'{name}-{fname}.nii.gz'
Nifti1Image(atlas_data, affine_eye * 3).to_filename(target_atlas_nii)
atlas_instance = fsl_fetcher(fname, data_dir=tmp_path, symmetric_split=split)
validate_atlas(atlas_instance)
_test_atlas_instance_should_match_data(atlas_instance, is_symm=is_symm or split)
for label in atlas_instance.labels:
    assert label.strip() == label
```

## Next Steps


---

*Source: test_atlas.py:236 | Complexity: Advanced | Last updated: 2026-05-18*