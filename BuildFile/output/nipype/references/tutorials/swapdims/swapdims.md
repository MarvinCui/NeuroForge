# How To: Swapdims

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test swapdims

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
files, testdir, out_ext = create_files_in_directory_plus_output_type
```

**Verification:**
```python
assert swap.cmd == 'fslswapdim'
```

### Step 2: Assign swap = fsl.SwapDimensions(...)

```python
swap = fsl.SwapDimensions()
```

**Verification:**
```python
assert swap.cmdline == 'fslswapdim a.nii x y z %s' % os.path.realpath(os.path.join(testdir, 'a_newdims%s' % out_ext))
```

### Step 3: Assign args = value

```python
args = [dict(in_file=files[0]), dict(new_dims=('x', 'y', 'z'))]
```

**Verification:**
```python
assert swap.cmdline == 'fslswapdim a.nii x y z b.nii'
```

### Step 4: Assign swap.inputs.in_file = value

```python
swap.inputs.in_file = files[0]
```

### Step 5: Assign swap.inputs.new_dims = value

```python
swap.inputs.new_dims = ('x', 'y', 'z')
```

**Verification:**
```python
assert swap.cmdline == 'fslswapdim a.nii x y z %s' % os.path.realpath(os.path.join(testdir, 'a_newdims%s' % out_ext))
```

### Step 6: Assign swap.inputs.out_file = 'b.nii'

```python
swap.inputs.out_file = 'b.nii'
```

**Verification:**
```python
assert swap.cmdline == 'fslswapdim a.nii x y z b.nii'
```

### Step 7: Assign wontrun = fsl.SwapDimensions(...)

```python
wontrun = fsl.SwapDimensions(**arg)
```

### Step 8: Call wontrun.run()

```python
wontrun.run()
```


## Complete Example

```python
# Setup
# Fixtures: create_files_in_directory_plus_output_type

# Workflow
files, testdir, out_ext = create_files_in_directory_plus_output_type
swap = fsl.SwapDimensions()
assert swap.cmd == 'fslswapdim'
args = [dict(in_file=files[0]), dict(new_dims=('x', 'y', 'z'))]
for arg in args:
    wontrun = fsl.SwapDimensions(**arg)
    with pytest.raises(ValueError):
        wontrun.run()
swap.inputs.in_file = files[0]
swap.inputs.new_dims = ('x', 'y', 'z')
assert swap.cmdline == 'fslswapdim a.nii x y z %s' % os.path.realpath(os.path.join(testdir, 'a_newdims%s' % out_ext))
swap.inputs.out_file = 'b.nii'
assert swap.cmdline == 'fslswapdim a.nii x y z b.nii'
```

## Next Steps


---

*Source: test_utils.py:327 | Complexity: Advanced | Last updated: 2026-05-18*