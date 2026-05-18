# How To: Maths Base

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test maths base

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
assert maths.cmd == 'fslmaths'
```

### Step 2: Assign maths = fsl.MathsCommand(...)

```python
maths = fsl.MathsCommand()
```

**Verification:**
```python
assert maths.cmdline == f'fslmaths a.nii {os.path.join(testdir, out_file)}'
```

### Step 3: Assign maths.inputs.in_file = 'a.nii'

```python
maths.inputs.in_file = 'a.nii'
```

**Verification:**
```python
assert foo.cmdline == int_cmdline.format(dtype)
```

### Step 4: Assign out_file = value

```python
out_file = f'a_maths{out_ext}'
```

**Verification:**
```python
assert bar.cmdline == out_cmdline.format(dtype)
```

### Step 5: Assign dtypes = value

```python
dtypes = ['float', 'char', 'int', 'short', 'double', 'input']
```

**Verification:**
```python
assert foobar.cmdline == duo_cmdline.format(dtype, dtype)
```

### Step 6: Assign int_cmdline = value

```python
int_cmdline = 'fslmaths -dt {} a.nii ' + os.path.join(testdir, out_file)
```

**Verification:**
```python
assert maths.cmdline == 'fslmaths a.nii b.nii'
```

### Step 7: Assign out_cmdline = value

```python
out_cmdline = 'fslmaths a.nii ' + os.path.join(testdir, out_file) + ' -odt {}'
```

### Step 8: Assign duo_cmdline = value

```python
duo_cmdline = 'fslmaths -dt {} a.nii ' + os.path.join(testdir, out_file) + ' -odt {}'
```

### Step 9: Assign maths.inputs.out_file = 'b.nii'

```python
maths.inputs.out_file = 'b.nii'
```

**Verification:**
```python
assert maths.cmdline == 'fslmaths a.nii b.nii'
```

### Step 10: Call maths.run()

```python
maths.run()
```

### Step 11: Assign foo = fsl.MathsCommand(...)

```python
foo = fsl.MathsCommand(in_file='a.nii', internal_datatype=dtype)
```

**Verification:**
```python
assert foo.cmdline == int_cmdline.format(dtype)
```

### Step 12: Assign bar = fsl.MathsCommand(...)

```python
bar = fsl.MathsCommand(in_file='a.nii', output_datatype=dtype)
```

**Verification:**
```python
assert bar.cmdline == out_cmdline.format(dtype)
```

### Step 13: Assign foobar = fsl.MathsCommand(...)

```python
foobar = fsl.MathsCommand(in_file='a.nii', internal_datatype=dtype, output_datatype=dtype)
```

**Verification:**
```python
assert foobar.cmdline == duo_cmdline.format(dtype, dtype)
```


## Complete Example

```python
# Setup
# Fixtures: create_files_in_directory_plus_output_type

# Workflow
files, testdir, out_ext = create_files_in_directory_plus_output_type
maths = fsl.MathsCommand()
assert maths.cmd == 'fslmaths'
with pytest.raises(ValueError):
    maths.run()
maths.inputs.in_file = 'a.nii'
out_file = f'a_maths{out_ext}'
assert maths.cmdline == f'fslmaths a.nii {os.path.join(testdir, out_file)}'
dtypes = ['float', 'char', 'int', 'short', 'double', 'input']
int_cmdline = 'fslmaths -dt {} a.nii ' + os.path.join(testdir, out_file)
out_cmdline = 'fslmaths a.nii ' + os.path.join(testdir, out_file) + ' -odt {}'
duo_cmdline = 'fslmaths -dt {} a.nii ' + os.path.join(testdir, out_file) + ' -odt {}'
for dtype in dtypes:
    foo = fsl.MathsCommand(in_file='a.nii', internal_datatype=dtype)
    assert foo.cmdline == int_cmdline.format(dtype)
    bar = fsl.MathsCommand(in_file='a.nii', output_datatype=dtype)
    assert bar.cmdline == out_cmdline.format(dtype)
    foobar = fsl.MathsCommand(in_file='a.nii', internal_datatype=dtype, output_datatype=dtype)
    assert foobar.cmdline == duo_cmdline.format(dtype, dtype)
maths.inputs.out_file = 'b.nii'
assert maths.cmdline == 'fslmaths a.nii b.nii'
```

## Next Steps


---

*Source: test_maths.py:15 | Complexity: Advanced | Last updated: 2026-05-18*