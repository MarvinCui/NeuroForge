# How To: Erosion

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test erosion

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
assert erode.cmd == 'fslmaths'
```

### Step 2: Assign erode = fsl.ErodeImage(...)

```python
erode = fsl.ErodeImage(in_file='a.nii', out_file='b.nii')
```

**Verification:**
```python
assert erode.cmdline == 'fslmaths a.nii -ero b.nii'
```

### Step 3: Assign erode.inputs.minimum_filter = True

```python
erode.inputs.minimum_filter = True
```

**Verification:**
```python
assert erode.cmdline == 'fslmaths a.nii -eroF b.nii'
```

### Step 4: Assign erode = fsl.ErodeImage(...)

```python
erode = fsl.ErodeImage(in_file='a.nii')
```

**Verification:**
```python
assert erode.cmdline == 'fslmaths a.nii -ero {}'.format(os.path.join(testdir, f'a_ero{out_ext}'))
```


## Complete Example

```python
# Setup
# Fixtures: create_files_in_directory_plus_output_type

# Workflow
files, testdir, out_ext = create_files_in_directory_plus_output_type
erode = fsl.ErodeImage(in_file='a.nii', out_file='b.nii')
assert erode.cmd == 'fslmaths'
assert erode.cmdline == 'fslmaths a.nii -ero b.nii'
erode.inputs.minimum_filter = True
assert erode.cmdline == 'fslmaths a.nii -eroF b.nii'
erode = fsl.ErodeImage(in_file='a.nii')
assert erode.cmdline == 'fslmaths a.nii -ero {}'.format(os.path.join(testdir, f'a_ero{out_ext}'))
```

## Next Steps


---

*Source: test_maths.py:302 | Complexity: Intermediate | Last updated: 2026-05-18*