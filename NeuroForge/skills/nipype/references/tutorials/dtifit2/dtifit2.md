# How To: Dtifit2

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test dtifit2

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `nipype.interfaces.fsl.dti`
- `nipype.interfaces.fsl`
- `nipype.interfaces.base`
- `pytest`
- `nipype.testing.fixtures`

**Setup Required:**
```python
# Fixtures: create_files_in_directory
```

## Step-by-Step Guide

### Step 1: Assign unknown = create_files_in_directory

```python
filelist, outdir = create_files_in_directory
```

**Verification:**
```python
assert dti.cmd == 'dtifit'
```

### Step 2: Assign dti = fsl.DTIFit(...)

```python
dti = fsl.DTIFit()
```

**Verification:**
```python
assert dti.cmdline == 'dtifit -k %s -o foo.dti.nii -m %s -r %s -b %s -Z 50 -z 10' % (filelist[0], filelist[1], filelist[0], filelist[1])
```

### Step 3: Assign dti.inputs.dwi = value

```python
dti.inputs.dwi = filelist[0]
```

### Step 4: Assign dti.inputs.base_name = 'foo.dti.nii'

```python
dti.inputs.base_name = 'foo.dti.nii'
```

### Step 5: Assign dti.inputs.mask = value

```python
dti.inputs.mask = filelist[1]
```

### Step 6: Assign dti.inputs.bvecs = value

```python
dti.inputs.bvecs = filelist[0]
```

### Step 7: Assign dti.inputs.bvals = value

```python
dti.inputs.bvals = filelist[1]
```

### Step 8: Assign dti.inputs.min_z = 10

```python
dti.inputs.min_z = 10
```

### Step 9: Assign dti.inputs.max_z = 50

```python
dti.inputs.max_z = 50
```

**Verification:**
```python
assert dti.cmdline == 'dtifit -k %s -o foo.dti.nii -m %s -r %s -b %s -Z 50 -z 10' % (filelist[0], filelist[1], filelist[0], filelist[1])
```

### Step 10: Call dti.run()

```python
dti.run()
```


## Complete Example

```python
# Setup
# Fixtures: create_files_in_directory

# Workflow
filelist, outdir = create_files_in_directory
dti = fsl.DTIFit()
assert dti.cmd == 'dtifit'
with pytest.raises(ValueError):
    dti.run()
dti.inputs.dwi = filelist[0]
dti.inputs.base_name = 'foo.dti.nii'
dti.inputs.mask = filelist[1]
dti.inputs.bvecs = filelist[0]
dti.inputs.bvals = filelist[1]
dti.inputs.min_z = 10
dti.inputs.max_z = 50
assert dti.cmdline == 'dtifit -k %s -o foo.dti.nii -m %s -r %s -b %s -Z 50 -z 10' % (filelist[0], filelist[1], filelist[0], filelist[1])
```

## Next Steps


---

*Source: test_dti.py:15 | Complexity: Advanced | Last updated: 2026-05-18*