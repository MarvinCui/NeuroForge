# How To: Fslmaths

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test fslmaths

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `numpy`
- `pytest`
- `nipype.interfaces.fsl.utils`
- `nipype.interfaces.fsl`
- `nipype.testing.fixtures`

**Setup Required:**
```python
# Fixtures: create_files_in_directory_plus_output_type
```

## Step-by-Step Guide

### Step 1: Assign unknown = create_files_in_directory_plus_output_type

```python
filelist, outdir, _ = create_files_in_directory_plus_output_type
```

**Verification:**
```python
assert math.cmd == 'fslmaths'
```

### Step 2: Assign math = fsl.ImageMaths(...)

```python
math = fsl.ImageMaths()
```

**Verification:**
```python
assert math.cmdline == 'fslmaths %s -add 2.5 -mul input_volume2 foo_math.nii' % filelist[0]
```

### Step 3: Assign math.inputs.in_file = value

```python
math.inputs.in_file = filelist[0]
```

**Verification:**
```python
assert math2.cmdline == 'fslmaths %s -add 2.5 foo2_math.nii' % filelist[0]
```

### Step 4: Assign math.inputs.op_string = '-add 2.5 -mul input_volume2'

```python
math.inputs.op_string = '-add 2.5 -mul input_volume2'
```

### Step 5: Assign math.inputs.out_file = 'foo_math.nii'

```python
math.inputs.out_file = 'foo_math.nii'
```

**Verification:**
```python
assert math.cmdline == 'fslmaths %s -add 2.5 -mul input_volume2 foo_math.nii' % filelist[0]
```

### Step 6: Assign math2 = fsl.ImageMaths(...)

```python
math2 = fsl.ImageMaths(in_file=filelist[0], op_string='-add 2.5', out_file='foo2_math.nii')
```

**Verification:**
```python
assert math2.cmdline == 'fslmaths %s -add 2.5 foo2_math.nii' % filelist[0]
```

### Step 7: Call math.run()

```python
math.run()
```


## Complete Example

```python
# Setup
# Fixtures: create_files_in_directory_plus_output_type

# Workflow
filelist, outdir, _ = create_files_in_directory_plus_output_type
math = fsl.ImageMaths()
assert math.cmd == 'fslmaths'
with pytest.raises(ValueError):
    math.run()
math.inputs.in_file = filelist[0]
math.inputs.op_string = '-add 2.5 -mul input_volume2'
math.inputs.out_file = 'foo_math.nii'
assert math.cmdline == 'fslmaths %s -add 2.5 -mul input_volume2 foo_math.nii' % filelist[0]
math2 = fsl.ImageMaths(in_file=filelist[0], op_string='-add 2.5', out_file='foo2_math.nii')
assert math2.cmdline == 'fslmaths %s -add 2.5 foo2_math.nii' % filelist[0]
```

## Next Steps


---

*Source: test_utils.py:103 | Complexity: Intermediate | Last updated: 2026-05-18*