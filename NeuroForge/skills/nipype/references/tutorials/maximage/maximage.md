# How To: Maximage

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test maximage

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
assert maxer.cmd == 'fslmaths'
```

### Step 2: Assign maxer = fsl.MaxImage(...)

```python
maxer = fsl.MaxImage(in_file='a.nii', out_file='b.nii')
```

**Verification:**
```python
assert maxer.cmdline == 'fslmaths a.nii -Tmax b.nii'
```

### Step 3: Assign cmdline = 'fslmaths a.nii -{}max b.nii'

```python
cmdline = 'fslmaths a.nii -{}max b.nii'
```

**Verification:**
```python
assert maxer.cmdline == cmdline.format(dim)
```

### Step 4: Assign maxer = fsl.MaxImage(...)

```python
maxer = fsl.MaxImage(in_file='a.nii')
```

**Verification:**
```python
assert maxer.cmdline == 'fslmaths a.nii -Tmax {}'.format(os.path.join(testdir, f'a_max{out_ext}'))
```

### Step 5: Assign maxer.inputs.dimension = dim

```python
maxer.inputs.dimension = dim
```

**Verification:**
```python
assert maxer.cmdline == cmdline.format(dim)
```


## Complete Example

```python
# Setup
# Fixtures: create_files_in_directory_plus_output_type

# Workflow
files, testdir, out_ext = create_files_in_directory_plus_output_type
maxer = fsl.MaxImage(in_file='a.nii', out_file='b.nii')
assert maxer.cmd == 'fslmaths'
assert maxer.cmdline == 'fslmaths a.nii -Tmax b.nii'
cmdline = 'fslmaths a.nii -{}max b.nii'
for dim in ['X', 'Y', 'Z', 'T']:
    maxer.inputs.dimension = dim
    assert maxer.cmdline == cmdline.format(dim)
maxer = fsl.MaxImage(in_file='a.nii')
assert maxer.cmdline == 'fslmaths a.nii -Tmax {}'.format(os.path.join(testdir, f'a_max{out_ext}'))
```

## Next Steps


---

*Source: test_maths.py:177 | Complexity: Intermediate | Last updated: 2026-05-18*