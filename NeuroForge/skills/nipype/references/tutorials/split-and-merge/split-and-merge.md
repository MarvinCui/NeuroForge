# How To: Split And Merge

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test split and merge

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `nipype.testing`
- `numpy`
- `nibabel`
- `nipype.algorithms.misc`

**Setup Required:**
```python
# Fixtures: tmpdir
```

## Step-by-Step Guide

### Step 1: Assign in_mask = example_data(...)

```python
in_mask = example_data('tpms_msk.nii.gz')
```

**Verification:**
```python
assert np.allclose(dwmasked, dwmerged)
```

### Step 2: Assign dwfile = value

```python
dwfile = tmpdir.join('dwi.nii.gz').strpath
```

### Step 3: Assign mask_img = nb.load(...)

```python
mask_img = nb.load(in_mask)
```

### Step 4: Assign mskdata = np.asanyarray(...)

```python
mskdata = np.asanyarray(mask_img.dataobj)
```

### Step 5: Assign aff = value

```python
aff = mask_img.affine
```

### Step 6: Assign dwshape = value

```python
dwshape = (mskdata.shape[0], mskdata.shape[1], mskdata.shape[2], 6)
```

### Step 7: Assign dwdata = np.random.normal(...)

```python
dwdata = np.random.normal(size=dwshape)
```

### Step 8: Call tmpdir.chdir()

```python
tmpdir.chdir()
```

### Step 9: Call nb.Nifti1Image.to_filename()

```python
nb.Nifti1Image(dwdata.astype(np.float32), aff, None).to_filename(dwfile)
```

### Step 10: Assign unknown = split_rois(...)

```python
resdw, resmsk, resid = split_rois(dwfile, in_mask, roishape=(20, 20, 2))
```

### Step 11: Assign merged = merge_rois(...)

```python
merged = merge_rois(resdw, resid, in_mask)
```

### Step 12: Assign dwmerged = nb.load.get_fdata(...)

```python
dwmerged = nb.load(merged).get_fdata(dtype=np.float32)
```

### Step 13: Assign dwmasked = value

```python
dwmasked = dwdata * mskdata[:, :, :, np.newaxis]
```

**Verification:**
```python
assert np.allclose(dwmasked, dwmerged)
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
import numpy as np
import nibabel as nb
from nipype.algorithms.misc import split_rois, merge_rois
in_mask = example_data('tpms_msk.nii.gz')
dwfile = tmpdir.join('dwi.nii.gz').strpath
mask_img = nb.load(in_mask)
mskdata = np.asanyarray(mask_img.dataobj)
aff = mask_img.affine
dwshape = (mskdata.shape[0], mskdata.shape[1], mskdata.shape[2], 6)
dwdata = np.random.normal(size=dwshape)
tmpdir.chdir()
nb.Nifti1Image(dwdata.astype(np.float32), aff, None).to_filename(dwfile)
resdw, resmsk, resid = split_rois(dwfile, in_mask, roishape=(20, 20, 2))
merged = merge_rois(resdw, resid, in_mask)
dwmerged = nb.load(merged).get_fdata(dtype=np.float32)
dwmasked = dwdata * mskdata[:, :, :, np.newaxis]
assert np.allclose(dwmasked, dwmerged)
```

## Next Steps


---

*Source: test_splitmerge.py:6 | Complexity: Advanced | Last updated: 2026-05-18*