# How To: Mask

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test mask

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
assert masker.cmd == 'fslmaths'
```

### Step 2: Assign masker = fsl.ApplyMask(...)

```python
masker = fsl.ApplyMask(in_file='a.nii', out_file='c.nii')
```

**Verification:**
```python
assert masker.cmdline == 'fslmaths a.nii -mas b.nii c.nii'
```

### Step 3: Assign masker.inputs.mask_file = 'b.nii'

```python
masker.inputs.mask_file = 'b.nii'
```

**Verification:**
```python
assert masker.cmdline == 'fslmaths a.nii -mas b.nii ' + os.path.join(testdir, f'a_masked{out_ext}')
```

### Step 4: Assign masker = fsl.ApplyMask(...)

```python
masker = fsl.ApplyMask(in_file='a.nii', mask_file='b.nii')
```

**Verification:**
```python
assert masker.cmdline == 'fslmaths a.nii -mas b.nii ' + os.path.join(testdir, f'a_masked{out_ext}')
```

### Step 5: Call masker.run()

```python
masker.run()
```


## Complete Example

```python
# Setup
# Fixtures: create_files_in_directory_plus_output_type

# Workflow
files, testdir, out_ext = create_files_in_directory_plus_output_type
masker = fsl.ApplyMask(in_file='a.nii', out_file='c.nii')
assert masker.cmd == 'fslmaths'
with pytest.raises(ValueError):
    masker.run()
masker.inputs.mask_file = 'b.nii'
assert masker.cmdline == 'fslmaths a.nii -mas b.nii c.nii'
masker = fsl.ApplyMask(in_file='a.nii', mask_file='b.nii')
assert masker.cmdline == 'fslmaths a.nii -mas b.nii ' + os.path.join(testdir, f'a_masked{out_ext}')
```

## Next Steps


---

*Source: test_maths.py:233 | Complexity: Intermediate | Last updated: 2026-05-18*