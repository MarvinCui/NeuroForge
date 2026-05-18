# How To: Head To Mni

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test conversion of aseg vertices to MNI coordinates.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne`
- `mne._freesurfer`
- `mne.datasets`
- `mne.transforms`


## Step-by-Step Guide

### Step 1: 'Test conversion of aseg vertices to MNI coordinates.'

```python
'Test conversion of aseg vertices to MNI coordinates.'
```

**Verification:**
```python
assert_allclose(coords_MNI, coords_MNI_2, atol=10.0)
```

### Step 2: Assign coords = value

```python
coords = np.array([[22.52, 11.24, 17.72], [22.52, 5.46, 21.58], [16.1, 5.46, 22.23], [21.24, 8.36, 22.23]]) / 1000.0
```

### Step 3: Assign xfm = read_talxfm(...)

```python
xfm = read_talxfm('sample', subjects_dir)
```

### Step 4: Assign coords_MNI = value

```python
coords_MNI = apply_trans(xfm['trans'], coords) * 1000.0
```

### Step 5: Assign unknown = _get_trans(...)

```python
mri_head_t, _ = _get_trans(trans_fname, 'mri', 'head', allow_none=False)
```

### Step 6: Assign coo_right_amygdala = np.array(...)

```python
coo_right_amygdala = np.array([[0.01745682, 0.02665809, 0.03281873], [0.01014125, 0.02496262, 0.04233755], [0.01713642, 0.02505193, 0.04258181], [0.01720631, 0.03073877, 0.03850075]])
```

### Step 7: Assign coords_MNI_2 = head_to_mni(...)

```python
coords_MNI_2 = head_to_mni(coo_right_amygdala, 'sample', mri_head_t, subjects_dir)
```

### Step 8: Call assert_allclose()

```python
assert_allclose(coords_MNI, coords_MNI_2, atol=10.0)
```


## Complete Example

```python
# Workflow
'Test conversion of aseg vertices to MNI coordinates.'
coords = np.array([[22.52, 11.24, 17.72], [22.52, 5.46, 21.58], [16.1, 5.46, 22.23], [21.24, 8.36, 22.23]]) / 1000.0
xfm = read_talxfm('sample', subjects_dir)
coords_MNI = apply_trans(xfm['trans'], coords) * 1000.0
mri_head_t, _ = _get_trans(trans_fname, 'mri', 'head', allow_none=False)
coo_right_amygdala = np.array([[0.01745682, 0.02665809, 0.03281873], [0.01014125, 0.02496262, 0.04233755], [0.01713642, 0.02505193, 0.04258181], [0.01720631, 0.03073877, 0.03850075]])
coords_MNI_2 = head_to_mni(coo_right_amygdala, 'sample', mri_head_t, subjects_dir)
assert_allclose(coords_MNI, coords_MNI_2, atol=10.0)
```

## Next Steps


---

*Source: test_freesurfer.py:76 | Complexity: Advanced | Last updated: 2026-05-18*