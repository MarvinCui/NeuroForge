# How To: Dilation

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test dilation

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
assert diller.cmd == 'fslmaths'
```

### Step 2: Assign diller = fsl.DilateImage(...)

```python
diller = fsl.DilateImage(in_file='a.nii', out_file='b.nii')
```

**Verification:**
```python
assert diller.cmdline == f'fslmaths a.nii -dil{cv[op]} b.nii'
```

### Step 3: Assign f = open.close(...)

```python
f = open('kernel.txt', 'w').close()
```

**Verification:**
```python
assert diller.cmdline == f'fslmaths a.nii -kernel {k} {size:.4f} -dilF b.nii'
```

### Step 4: Assign diller.inputs.kernel_shape = 'file'

```python
diller.inputs.kernel_shape = 'file'
```

**Verification:**
```python
assert diller.cmdline == 'fslmaths a.nii -kernel file kernel.txt -dilF b.nii'
```

### Step 5: Assign diller.inputs.kernel_size = Undefined

```python
diller.inputs.kernel_size = Undefined
```

**Verification:**
```python
assert dil.cmdline == 'fslmaths a.nii -dilF {}'.format(os.path.join(testdir, f'a_dil{out_ext}'))
```

### Step 6: Assign diller.inputs.kernel_file = 'kernel.txt'

```python
diller.inputs.kernel_file = 'kernel.txt'
```

**Verification:**
```python
assert diller.cmdline == 'fslmaths a.nii -kernel file kernel.txt -dilF b.nii'
```

### Step 7: Assign dil = fsl.DilateImage(...)

```python
dil = fsl.DilateImage(in_file='a.nii', operation='max')
```

**Verification:**
```python
assert dil.cmdline == 'fslmaths a.nii -dilF {}'.format(os.path.join(testdir, f'a_dil{out_ext}'))
```

### Step 8: Call diller.run()

```python
diller.run()
```

### Step 9: Assign cv = dict(...)

```python
cv = dict(mean='M', modal='D', max='F')
```

### Step 10: Assign diller.inputs.operation = op

```python
diller.inputs.operation = op
```

**Verification:**
```python
assert diller.cmdline == f'fslmaths a.nii -dil{cv[op]} b.nii'
```

### Step 11: Assign diller.inputs.kernel_shape = k

```python
diller.inputs.kernel_shape = k
```

### Step 12: Assign diller.inputs.kernel_size = size

```python
diller.inputs.kernel_size = size
```

**Verification:**
```python
assert diller.cmdline == f'fslmaths a.nii -kernel {k} {size:.4f} -dilF b.nii'
```


## Complete Example

```python
# Setup
# Fixtures: create_files_in_directory_plus_output_type

# Workflow
files, testdir, out_ext = create_files_in_directory_plus_output_type
diller = fsl.DilateImage(in_file='a.nii', out_file='b.nii')
assert diller.cmd == 'fslmaths'
with pytest.raises(ValueError):
    diller.run()
for op in ['mean', 'modal', 'max']:
    cv = dict(mean='M', modal='D', max='F')
    diller.inputs.operation = op
    assert diller.cmdline == f'fslmaths a.nii -dil{cv[op]} b.nii'
for k in ['3D', '2D', 'box', 'boxv', 'gauss', 'sphere']:
    for size in [1, 1.5, 5]:
        diller.inputs.kernel_shape = k
        diller.inputs.kernel_size = size
        assert diller.cmdline == f'fslmaths a.nii -kernel {k} {size:.4f} -dilF b.nii'
f = open('kernel.txt', 'w').close()
del f
diller.inputs.kernel_shape = 'file'
diller.inputs.kernel_size = Undefined
diller.inputs.kernel_file = 'kernel.txt'
assert diller.cmdline == 'fslmaths a.nii -kernel file kernel.txt -dilF b.nii'
dil = fsl.DilateImage(in_file='a.nii', operation='max')
assert dil.cmdline == 'fslmaths a.nii -dilF {}'.format(os.path.join(testdir, f'a_dil{out_ext}'))
```

## Next Steps


---

*Source: test_maths.py:258 | Complexity: Advanced | Last updated: 2026-05-18*