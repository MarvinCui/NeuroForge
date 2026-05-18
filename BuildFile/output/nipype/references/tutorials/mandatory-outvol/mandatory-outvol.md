# How To: Mandatory Outvol

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test mandatory outvol

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `pytest`
- `looseversion`
- `nipype.testing.fixtures`
- `nipype.interfaces`
- `nipype.interfaces.freesurfer`

**Setup Required:**
```python
# Fixtures: create_files_in_directory
```

## Step-by-Step Guide

### Step 1: Assign unknown = create_files_in_directory

```python
filelist, outdir = create_files_in_directory
```

**Verification:**
```python
assert mni.cmd == 'mri_nu_correct.mni'
```

### Step 2: Assign mni = freesurfer.MNIBiasCorrection(...)

```python
mni = freesurfer.MNIBiasCorrection()
```

**Verification:**
```python
assert mni.cmdline == f'mri_nu_correct.mni --i {filelist[0]} --n 4 --o {base}_output{ext}'
```

### Step 3: Assign mni.inputs.in_file = value

```python
mni.inputs.in_file = filelist[0]
```

**Verification:**
```python
assert mni.cmdline == 'mri_nu_correct.mni --i %s --n 4 --o new_corrected_file.mgz' % filelist[0]
```

### Step 4: Assign unknown = os.path.splitext(...)

```python
base, ext = os.path.splitext(os.path.basename(filelist[0]))
```

**Verification:**
```python
assert mni2.cmdline == 'mri_nu_correct.mni --i %s --n 2 --o bias_corrected_output' % filelist[0]
```

### Step 5: Assign mni.inputs.out_file = 'new_corrected_file.mgz'

```python
mni.inputs.out_file = 'new_corrected_file.mgz'
```

**Verification:**
```python
assert mni.cmdline == 'mri_nu_correct.mni --i %s --n 4 --o new_corrected_file.mgz' % filelist[0]
```

### Step 6: Assign mni2 = freesurfer.MNIBiasCorrection(...)

```python
mni2 = freesurfer.MNIBiasCorrection(in_file=filelist[0], out_file='bias_corrected_output', iterations=2)
```

**Verification:**
```python
assert mni2.cmdline == 'mri_nu_correct.mni --i %s --n 2 --o bias_corrected_output' % filelist[0]
```

### Step 7: mni.cmdline

```python
mni.cmdline
```

### Step 8: Assign unknown = os.path.splitext(...)

```python
base, ext2 = os.path.splitext(base)
```

### Step 9: Assign ext = value

```python
ext = ext2 + ext
```


## Complete Example

```python
# Setup
# Fixtures: create_files_in_directory

# Workflow
filelist, outdir = create_files_in_directory
mni = freesurfer.MNIBiasCorrection()
assert mni.cmd == 'mri_nu_correct.mni'
with pytest.raises(ValueError):
    mni.cmdline
mni.inputs.in_file = filelist[0]
base, ext = os.path.splitext(os.path.basename(filelist[0]))
if ext == '.gz':
    base, ext2 = os.path.splitext(base)
    ext = ext2 + ext
assert mni.cmdline == f'mri_nu_correct.mni --i {filelist[0]} --n 4 --o {base}_output{ext}'
mni.inputs.out_file = 'new_corrected_file.mgz'
assert mni.cmdline == 'mri_nu_correct.mni --i %s --n 4 --o new_corrected_file.mgz' % filelist[0]
mni2 = freesurfer.MNIBiasCorrection(in_file=filelist[0], out_file='bias_corrected_output', iterations=2)
assert mni2.cmdline == 'mri_nu_correct.mni --i %s --n 2 --o bias_corrected_output' % filelist[0]
```

## Next Steps


---

*Source: test_preprocess.py:120 | Complexity: Advanced | Last updated: 2026-05-18*