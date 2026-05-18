# How To: Stdimage

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test stdimage

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `numpy`
- `nipype.interfaces.base`
- `nipype.interfaces.fsl.maths`
- `nipype.interfaces.fsl`
- `pytest`
- `nipype.testing.fixtures`

**Setup Required:**
```python
# Fixtures: create_files_in_directory_plus_output_type
```

## Step-by-Step Guide

### Step 1: Assign unknown = create_files_in_directory_plus_output_type

```python
files, testdir, out_ext = create_files_in_directory_plus_output_type
```

**Verification:**
```python
assert stder.cmd == 'fslmaths'
```

### Step 2: Assign stder = fsl.StdImage(...)

```python
stder = fsl.StdImage(in_file='a.nii', out_file='b.nii')
```

**Verification:**
```python
assert stder.cmdline == 'fslmaths a.nii -Tstd b.nii'
```

### Step 3: Assign cmdline = 'fslmaths a.nii -{}std b.nii'

```python
cmdline = 'fslmaths a.nii -{}std b.nii'
```

**Verification:**
```python
assert stder.cmdline == cmdline.format(dim)
```

### Step 4: Assign stder = fsl.StdImage(...)

```python
stder = fsl.StdImage(in_file='a.nii', output_type='NIFTI')
```

**Verification:**
```python
assert stder.cmdline == 'fslmaths a.nii -Tstd {}'.format(os.path.join(testdir, 'a_std.nii'))
```

### Step 5: Assign stder.inputs.dimension = dim

```python
stder.inputs.dimension = dim
```

**Verification:**
```python
assert stder.cmdline == cmdline.format(dim)
```


## Complete Example

```python
# Setup
# Fixtures: create_files_in_directory_plus_output_type

# Workflow
files, testdir, out_ext = create_files_in_directory_plus_output_type
stder = fsl.StdImage(in_file='a.nii', out_file='b.nii')
assert stder.cmd == 'fslmaths'
assert stder.cmdline == 'fslmaths a.nii -Tstd b.nii'
cmdline = 'fslmaths a.nii -{}std b.nii'
for dim in ['X', 'Y', 'Z', 'T']:
    stder.inputs.dimension = dim
    assert stder.cmdline == cmdline.format(dim)
stder = fsl.StdImage(in_file='a.nii', output_type='NIFTI')
assert stder.cmdline == 'fslmaths a.nii -Tstd {}'.format(os.path.join(testdir, 'a_std.nii'))
```

## Next Steps


---

*Source: test_maths.py:151 | Complexity: Intermediate | Last updated: 2026-05-18*