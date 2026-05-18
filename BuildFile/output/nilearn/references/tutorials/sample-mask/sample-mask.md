# How To: Sample Mask

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test load method and sample mask.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `re`
- `numpy`
- `pandas`
- `pytest`
- `nibabel`
- `scipy.stats`
- `sklearn.preprocessing`
- `nilearn._utils.data_gen`
- `nilearn._utils.fmriprep_confounds`
- `nilearn.conftest`
- `nilearn.interfaces.bids`
- `nilearn.interfaces.fmriprep`
- `nilearn.interfaces.fmriprep.load_confounds`
- `nilearn.interfaces.fmriprep.tests._testing`
- `nilearn.maskers`
- `nilearn.tests.test_signal`
- `inspect`

**Setup Required:**
```python
# Fixtures: tmp_path, fmriprep_version, scrubbed_time_points, non_steady_outliers
```

## Step-by-Step Guide

### Step 1: 'Test load method and sample mask.'

```python
'Test load method and sample mask.'
```

**Verification:**
```python
assert reg.shape[0] - len(mask) == scrubbed_time_points
```

### Step 2: Assign unknown = create_tmp_filepath(...)

```python
regular_nii, regular_conf = create_tmp_filepath(tmp_path, image_type='regular', copy_confounds=True, fmriprep_version=fmriprep_version)
```

**Verification:**
```python
assert reg.shape[0] == 30
```

### Step 3: Assign unknown = load_confounds(...)

```python
reg, mask = load_confounds(regular_nii, strategy=('motion', 'scrub'), scrub=5, fd_threshold=0.15)
```

**Verification:**
```python
assert reg.shape[0] - len(mask) == non_steady_outliers
```

### Step 4: Assign unknown = load_confounds(...)

```python
reg, mask = load_confounds(regular_nii, strategy=('motion',))
```

**Verification:**
```python
assert mask is None
```

### Step 5: Assign unknown = get_legal_confound(...)

```python
conf_data, _ = get_legal_confound(non_steady_state=False)
```

**Verification:**
```python
assert mask is None
```

### Step 6: Call conf_data.to_csv()

```python
conf_data.to_csv(regular_conf, sep='\t', index=False)
```

### Step 7: Assign unknown = load_confounds(...)

```python
reg, mask = load_confounds(regular_nii, strategy=('motion',))
```

**Verification:**
```python
assert mask is None
```

### Step 8: Assign unknown = load_confounds(...)

```python
reg, mask = load_confounds(regular_nii, strategy=('motion', 'scrub'), scrub=0, fd_threshold=4)
```

**Verification:**
```python
assert mask is None
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, fmriprep_version, scrubbed_time_points, non_steady_outliers

# Workflow
'Test load method and sample mask.'
regular_nii, regular_conf = create_tmp_filepath(tmp_path, image_type='regular', copy_confounds=True, fmriprep_version=fmriprep_version)
reg, mask = load_confounds(regular_nii, strategy=('motion', 'scrub'), scrub=5, fd_threshold=0.15)
assert reg.shape[0] - len(mask) == scrubbed_time_points
assert reg.shape[0] == 30
reg, mask = load_confounds(regular_nii, strategy=('motion',))
assert reg.shape[0] - len(mask) == non_steady_outliers
conf_data, _ = get_legal_confound(non_steady_state=False)
conf_data.to_csv(regular_conf, sep='\t', index=False)
reg, mask = load_confounds(regular_nii, strategy=('motion',))
assert mask is None
reg, mask = load_confounds(regular_nii, strategy=('motion', 'scrub'), scrub=0, fd_threshold=4)
assert mask is None
```

## Next Steps


---

*Source: test_load_confounds.py:735 | Complexity: Advanced | Last updated: 2026-05-18*