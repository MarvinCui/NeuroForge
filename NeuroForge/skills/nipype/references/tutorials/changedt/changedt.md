# How To: Changedt

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test changedt

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
assert cdt.cmd == 'fslmaths'
```

### Step 2: Assign cdt = fsl.ChangeDataType(...)

```python
cdt = fsl.ChangeDataType()
```

**Verification:**
```python
assert foo.cmdline == cmdline.format(dtype)
```

### Step 3: Assign cdt.inputs.in_file = 'a.nii'

```python
cdt.inputs.in_file = 'a.nii'
```

### Step 4: Assign cdt.inputs.out_file = 'b.nii'

```python
cdt.inputs.out_file = 'b.nii'
```

### Step 5: Assign dtypes = value

```python
dtypes = ['float', 'char', 'int', 'short', 'double', 'input']
```

### Step 6: Assign cmdline = 'fslmaths a.nii b.nii -odt {}'

```python
cmdline = 'fslmaths a.nii b.nii -odt {}'
```

### Step 7: Call cdt.run()

```python
cdt.run()
```

### Step 8: Call cdt.run()

```python
cdt.run()
```

### Step 9: Assign foo = fsl.MathsCommand(...)

```python
foo = fsl.MathsCommand(in_file='a.nii', out_file='b.nii', output_datatype=dtype)
```

**Verification:**
```python
assert foo.cmdline == cmdline.format(dtype)
```


## Complete Example

```python
# Setup
# Fixtures: create_files_in_directory_plus_output_type

# Workflow
files, testdir, out_ext = create_files_in_directory_plus_output_type
cdt = fsl.ChangeDataType()
assert cdt.cmd == 'fslmaths'
with pytest.raises(ValueError):
    cdt.run()
cdt.inputs.in_file = 'a.nii'
cdt.inputs.out_file = 'b.nii'
with pytest.raises(ValueError):
    cdt.run()
dtypes = ['float', 'char', 'int', 'short', 'double', 'input']
cmdline = 'fslmaths a.nii b.nii -odt {}'
for dtype in dtypes:
    foo = fsl.MathsCommand(in_file='a.nii', out_file='b.nii', output_datatype=dtype)
    assert foo.cmdline == cmdline.format(dtype)
```

## Next Steps


---

*Source: test_maths.py:58 | Complexity: Advanced | Last updated: 2026-05-18*