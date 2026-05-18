# How To: Distancemap

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test distancemap

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

### Step 1: Assign mapper = fsl.DistanceMap(...)

```python
mapper = fsl.DistanceMap()
```

**Verification:**
```python
assert mapper.cmd == 'distancemap'
```

### Step 2: Assign unknown = create_files_in_directory

```python
files, newdir = create_files_in_directory
```

**Verification:**
```python
assert mapper.cmdline == 'distancemap --out=%s --in=a.nii' % os.path.join(newdir, 'a_dstmap.nii')
```

### Step 3: Assign mapper.inputs.in_file = 'a.nii'

```python
mapper.inputs.in_file = 'a.nii'
```

**Verification:**
```python
assert mapper.cmdline == 'distancemap --out={} --in=a.nii --localmax={}'.format(os.path.join(newdir, 'a_dstmap.nii'), os.path.join(newdir, 'a_lclmax.nii'))
```

### Step 4: Assign mapper.inputs.local_max_file = True

```python
mapper.inputs.local_max_file = True
```

**Verification:**
```python
assert mapper.cmdline == 'distancemap --out=%s --in=a.nii --localmax=max.nii' % os.path.join(newdir, 'a_dstmap.nii')
```

### Step 5: Assign mapper.inputs.local_max_file = 'max.nii'

```python
mapper.inputs.local_max_file = 'max.nii'
```

**Verification:**
```python
assert mapper.cmdline == 'distancemap --out=%s --in=a.nii --localmax=max.nii' % os.path.join(newdir, 'a_dstmap.nii')
```

### Step 6: Call mapper.run()

```python
mapper.run()
```


## Complete Example

```python
# Setup
# Fixtures: create_files_in_directory

# Workflow
mapper = fsl.DistanceMap()
files, newdir = create_files_in_directory
assert mapper.cmd == 'distancemap'
with pytest.raises(ValueError):
    mapper.run()
mapper.inputs.in_file = 'a.nii'
assert mapper.cmdline == 'distancemap --out=%s --in=a.nii' % os.path.join(newdir, 'a_dstmap.nii')
mapper.inputs.local_max_file = True
assert mapper.cmdline == 'distancemap --out={} --in=a.nii --localmax={}'.format(os.path.join(newdir, 'a_dstmap.nii'), os.path.join(newdir, 'a_lclmax.nii'))
mapper.inputs.local_max_file = 'max.nii'
assert mapper.cmdline == 'distancemap --out=%s --in=a.nii --localmax=max.nii' % os.path.join(newdir, 'a_dstmap.nii')
```

## Next Steps


---

*Source: test_dti.py:389 | Complexity: Intermediate | Last updated: 2026-05-18*