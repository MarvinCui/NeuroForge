# How To: Threshold

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test threshold

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
assert thresh.cmd == 'fslmaths'
```

### Step 2: Assign thresh = fsl.Threshold(...)

```python
thresh = fsl.Threshold(in_file='a.nii', out_file='b.nii')
```

**Verification:**
```python
assert thresh.cmdline == cmdline.format(f'-thr {val:.10f}')
```

### Step 3: Assign cmdline = 'fslmaths a.nii {} b.nii'

```python
cmdline = 'fslmaths a.nii {} b.nii'
```

**Verification:**
```python
assert thresh.cmdline == cmdline.format('-thrp ' + val)
```

### Step 4: Assign val = value

```python
val = f'{42:.10f}'
```

**Verification:**
```python
assert thresh.cmdline == cmdline.format('-thrP ' + val)
```

### Step 5: Assign thresh = fsl.Threshold(...)

```python
thresh = fsl.Threshold(in_file='a.nii', out_file='b.nii', thresh=42, use_robust_range=True)
```

**Verification:**
```python
assert thresh.cmdline == cmdline.format('-uthr ' + val)
```

### Step 6: Assign thresh.inputs.use_nonzero_voxels = True

```python
thresh.inputs.use_nonzero_voxels = True
```

**Verification:**
```python
assert thresh.cmdline == cmdline.format('-uthrp ' + val)
```

### Step 7: Assign thresh = fsl.Threshold(...)

```python
thresh = fsl.Threshold(in_file='a.nii', out_file='b.nii', thresh=42, direction='above')
```

**Verification:**
```python
assert thresh.cmdline == cmdline.format('-uthrP ' + val)
```

### Step 8: Assign thresh.inputs.use_robust_range = True

```python
thresh.inputs.use_robust_range = True
```

**Verification:**
```python
assert thresh.cmdline == cmdline.format('-uthrp ' + val)
```

### Step 9: Assign thresh.inputs.use_nonzero_voxels = True

```python
thresh.inputs.use_nonzero_voxels = True
```

**Verification:**
```python
assert thresh.cmdline == cmdline.format('-uthrP ' + val)
```

### Step 10: Call thresh.run()

```python
thresh.run()
```

### Step 11: Assign thresh.inputs.thresh = val

```python
thresh.inputs.thresh = val
```

**Verification:**
```python
assert thresh.cmdline == cmdline.format(f'-thr {val:.10f}')
```


## Complete Example

```python
# Setup
# Fixtures: create_files_in_directory_plus_output_type

# Workflow
files, testdir, out_ext = create_files_in_directory_plus_output_type
thresh = fsl.Threshold(in_file='a.nii', out_file='b.nii')
assert thresh.cmd == 'fslmaths'
with pytest.raises(ValueError):
    thresh.run()
cmdline = 'fslmaths a.nii {} b.nii'
for val in [0, 0.0, -1, -1.5, -0.5, 0.5, 3, 400, 400.5]:
    thresh.inputs.thresh = val
    assert thresh.cmdline == cmdline.format(f'-thr {val:.10f}')
val = f'{42:.10f}'
thresh = fsl.Threshold(in_file='a.nii', out_file='b.nii', thresh=42, use_robust_range=True)
assert thresh.cmdline == cmdline.format('-thrp ' + val)
thresh.inputs.use_nonzero_voxels = True
assert thresh.cmdline == cmdline.format('-thrP ' + val)
thresh = fsl.Threshold(in_file='a.nii', out_file='b.nii', thresh=42, direction='above')
assert thresh.cmdline == cmdline.format('-uthr ' + val)
thresh.inputs.use_robust_range = True
assert thresh.cmdline == cmdline.format('-uthrp ' + val)
thresh.inputs.use_nonzero_voxels = True
assert thresh.cmdline == cmdline.format('-uthrP ' + val)
```

## Next Steps


---

*Source: test_maths.py:88 | Complexity: Advanced | Last updated: 2026-05-18*