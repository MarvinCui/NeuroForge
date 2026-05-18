# How To: Surfsmooth

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test surfsmooth

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `os.path`
- `pytest`
- `nipype.testing.fixtures`
- `nipype.pipeline`
- `nipype.interfaces`
- `nipype.interfaces.base`
- `nipype.interfaces.io`

**Setup Required:**
```python
# Fixtures: create_surf_file_in_directory
```

## Step-by-Step Guide

### Step 1: Assign smooth = fs.SurfaceSmooth(...)

```python
smooth = fs.SurfaceSmooth()
```

**Verification:**
```python
assert smooth.cmd == 'mri_surf2surf'
```

### Step 2: Assign unknown = create_surf_file_in_directory

```python
surf, cwd = create_surf_file_in_directory
```

**Verification:**
```python
assert smooth.cmdline == 'mri_surf2surf --cortex --fwhm 5.0000 --hemi lh --sval %s --tval %s/lh.a_smooth%d.nii --s fsaverage' % (surf, cwd, fwhm)
```

### Step 3: Assign smooth.inputs.in_file = surf

```python
smooth.inputs.in_file = surf
```

**Verification:**
```python
assert smooth != shmooth
```

### Step 4: Assign smooth.inputs.subject_id = 'fsaverage'

```python
smooth.inputs.subject_id = 'fsaverage'
```

### Step 5: Assign fwhm = 5

```python
fwhm = 5
```

### Step 6: Assign smooth.inputs.fwhm = fwhm

```python
smooth.inputs.fwhm = fwhm
```

### Step 7: Assign smooth.inputs.hemi = 'lh'

```python
smooth.inputs.hemi = 'lh'
```

**Verification:**
```python
assert smooth.cmdline == 'mri_surf2surf --cortex --fwhm 5.0000 --hemi lh --sval %s --tval %s/lh.a_smooth%d.nii --s fsaverage' % (surf, cwd, fwhm)
```

### Step 8: Assign shmooth = fs.SurfaceSmooth(...)

```python
shmooth = fs.SurfaceSmooth(subject_id='fsaverage', fwhm=6, in_file=surf, hemi='lh', out_file='lh.a_smooth.nii')
```

**Verification:**
```python
assert smooth != shmooth
```

### Step 9: Call smooth.run()

```python
smooth.run()
```


## Complete Example

```python
# Setup
# Fixtures: create_surf_file_in_directory

# Workflow
smooth = fs.SurfaceSmooth()
assert smooth.cmd == 'mri_surf2surf'
with pytest.raises(ValueError):
    smooth.run()
surf, cwd = create_surf_file_in_directory
smooth.inputs.in_file = surf
smooth.inputs.subject_id = 'fsaverage'
fwhm = 5
smooth.inputs.fwhm = fwhm
smooth.inputs.hemi = 'lh'
assert smooth.cmdline == 'mri_surf2surf --cortex --fwhm 5.0000 --hemi lh --sval %s --tval %s/lh.a_smooth%d.nii --s fsaverage' % (surf, cwd, fwhm)
shmooth = fs.SurfaceSmooth(subject_id='fsaverage', fwhm=6, in_file=surf, hemi='lh', out_file='lh.a_smooth.nii')
assert smooth != shmooth
```

## Next Steps


---

*Source: test_utils.py:65 | Complexity: Advanced | Last updated: 2026-05-18*