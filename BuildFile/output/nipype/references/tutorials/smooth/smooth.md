# How To: Smooth

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test smooth

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
assert smoother.cmd == 'fslmaths'
```

### Step 2: Assign smoother = fsl.IsotropicSmooth(...)

```python
smoother = fsl.IsotropicSmooth(in_file='a.nii', out_file='b.nii')
```

**Verification:**
```python
assert smoother.cmdline == cmdline.format(val)
```

### Step 3: Assign cmdline = 'fslmaths a.nii -s {:.5f} b.nii'

```python
cmdline = 'fslmaths a.nii -s {:.5f} b.nii'
```

**Verification:**
```python
assert smoother.cmdline == cmdline.format(val)
```

### Step 4: Assign smoother = fsl.IsotropicSmooth(...)

```python
smoother = fsl.IsotropicSmooth(in_file='a.nii', sigma=5)
```

**Verification:**
```python
assert smoother.cmdline == 'fslmaths a.nii -s {:.5f} {}'.format(5, os.path.join(testdir, f'a_smooth{out_ext}'))
```

### Step 5: Call smoother.run()

```python
smoother.run()
```

### Step 6: Assign smoother = fsl.IsotropicSmooth(...)

```python
smoother = fsl.IsotropicSmooth(in_file='a.nii', out_file='b.nii', sigma=val)
```

**Verification:**
```python
assert smoother.cmdline == cmdline.format(val)
```

### Step 7: Assign smoother = fsl.IsotropicSmooth(...)

```python
smoother = fsl.IsotropicSmooth(in_file='a.nii', out_file='b.nii', fwhm=val)
```

### Step 8: Assign val = value

```python
val = float(val) / np.sqrt(8 * np.log(2))
```

**Verification:**
```python
assert smoother.cmdline == cmdline.format(val)
```


## Complete Example

```python
# Setup
# Fixtures: create_files_in_directory_plus_output_type

# Workflow
files, testdir, out_ext = create_files_in_directory_plus_output_type
smoother = fsl.IsotropicSmooth(in_file='a.nii', out_file='b.nii')
assert smoother.cmd == 'fslmaths'
with pytest.raises(ValueError):
    smoother.run()
cmdline = 'fslmaths a.nii -s {:.5f} b.nii'
for val in [0, 1.0, 1, 25, 0.5, 8 / 3.0]:
    smoother = fsl.IsotropicSmooth(in_file='a.nii', out_file='b.nii', sigma=val)
    assert smoother.cmdline == cmdline.format(val)
    smoother = fsl.IsotropicSmooth(in_file='a.nii', out_file='b.nii', fwhm=val)
    val = float(val) / np.sqrt(8 * np.log(2))
    assert smoother.cmdline == cmdline.format(val)
smoother = fsl.IsotropicSmooth(in_file='a.nii', sigma=5)
assert smoother.cmdline == 'fslmaths a.nii -s {:.5f} {}'.format(5, os.path.join(testdir, f'a_smooth{out_ext}'))
```

## Next Steps


---

*Source: test_maths.py:203 | Complexity: Advanced | Last updated: 2026-05-18*