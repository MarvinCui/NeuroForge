# How To: Meanimage

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test meanimage

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
assert meaner.cmd == 'fslmaths'
```

### Step 2: Assign meaner = fsl.MeanImage(...)

```python
meaner = fsl.MeanImage(in_file='a.nii', out_file='b.nii')
```

**Verification:**
```python
assert meaner.cmdline == 'fslmaths a.nii -Tmean b.nii'
```

### Step 3: Assign cmdline = 'fslmaths a.nii -{}mean b.nii'

```python
cmdline = 'fslmaths a.nii -{}mean b.nii'
```

**Verification:**
```python
assert meaner.cmdline == cmdline.format(dim)
```

### Step 4: Assign meaner = fsl.MeanImage(...)

```python
meaner = fsl.MeanImage(in_file='a.nii')
```

**Verification:**
```python
assert meaner.cmdline == 'fslmaths a.nii -Tmean {}'.format(os.path.join(testdir, f'a_mean{out_ext}'))
```

### Step 5: Assign meaner.inputs.dimension = dim

```python
meaner.inputs.dimension = dim
```

**Verification:**
```python
assert meaner.cmdline == cmdline.format(dim)
```


## Complete Example

```python
# Setup
# Fixtures: create_files_in_directory_plus_output_type

# Workflow
files, testdir, out_ext = create_files_in_directory_plus_output_type
meaner = fsl.MeanImage(in_file='a.nii', out_file='b.nii')
assert meaner.cmd == 'fslmaths'
assert meaner.cmdline == 'fslmaths a.nii -Tmean b.nii'
cmdline = 'fslmaths a.nii -{}mean b.nii'
for dim in ['X', 'Y', 'Z', 'T']:
    meaner.inputs.dimension = dim
    assert meaner.cmdline == cmdline.format(dim)
meaner = fsl.MeanImage(in_file='a.nii')
assert meaner.cmdline == 'fslmaths a.nii -Tmean {}'.format(os.path.join(testdir, f'a_mean{out_ext}'))
```

## Next Steps


---

*Source: test_maths.py:125 | Complexity: Intermediate | Last updated: 2026-05-18*