# How To: Surfxfm

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test surfxfm

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

### Step 1: Assign xfm = fs.SurfaceTransform(...)

```python
xfm = fs.SurfaceTransform()
```

**Verification:**
```python
assert xfm.cmd == 'mri_surf2surf'
```

### Step 2: Assign unknown = create_surf_file_in_directory

```python
surf, cwd = create_surf_file_in_directory
```

**Verification:**
```python
assert xfm.cmdline == 'mri_surf2surf --hemi lh --tval %s/lh.a.fsaverage.nii --sval %s --srcsubject my_subject --trgsubject fsaverage' % (cwd, surf)
```

### Step 3: Assign xfm.inputs.source_file = surf

```python
xfm.inputs.source_file = surf
```

**Verification:**
```python
assert xfm != xfmish
```

### Step 4: Assign xfm.inputs.source_subject = 'my_subject'

```python
xfm.inputs.source_subject = 'my_subject'
```

### Step 5: Assign xfm.inputs.target_subject = 'fsaverage'

```python
xfm.inputs.target_subject = 'fsaverage'
```

### Step 6: Assign xfm.inputs.hemi = 'lh'

```python
xfm.inputs.hemi = 'lh'
```

**Verification:**
```python
assert xfm.cmdline == 'mri_surf2surf --hemi lh --tval %s/lh.a.fsaverage.nii --sval %s --srcsubject my_subject --trgsubject fsaverage' % (cwd, surf)
```

### Step 7: Assign xfmish = fs.SurfaceTransform(...)

```python
xfmish = fs.SurfaceTransform(source_subject='fsaverage', target_subject='my_subject', source_file=surf, hemi='lh')
```

**Verification:**
```python
assert xfm != xfmish
```

### Step 8: Call xfm.run()

```python
xfm.run()
```


## Complete Example

```python
# Setup
# Fixtures: create_surf_file_in_directory

# Workflow
xfm = fs.SurfaceTransform()
assert xfm.cmd == 'mri_surf2surf'
with pytest.raises(ValueError):
    xfm.run()
surf, cwd = create_surf_file_in_directory
xfm.inputs.source_file = surf
xfm.inputs.source_subject = 'my_subject'
xfm.inputs.target_subject = 'fsaverage'
xfm.inputs.hemi = 'lh'
assert xfm.cmdline == 'mri_surf2surf --hemi lh --tval %s/lh.a.fsaverage.nii --sval %s --srcsubject my_subject --trgsubject fsaverage' % (cwd, surf)
xfmish = fs.SurfaceTransform(source_subject='fsaverage', target_subject='my_subject', source_file=surf, hemi='lh')
assert xfm != xfmish
```

## Next Steps


---

*Source: test_utils.py:103 | Complexity: Advanced | Last updated: 2026-05-18*