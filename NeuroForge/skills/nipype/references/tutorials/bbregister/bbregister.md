# How To: Bbregister

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test bbregister

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `pytest`
- `looseversion`
- `nipype.testing.fixtures`
- `nipype.interfaces`
- `nipype.interfaces.freesurfer`

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
assert bbr.cmd == 'bbregister'
```

### Step 2: Assign bbr = freesurfer.BBRegister(...)

```python
bbr = freesurfer.BBRegister()
```

**Verification:**
```python
assert bbr.cmdline == 'bbregister --t2 --init-fsl --reg {base}_bbreg_fsaverage.dat --mov {full} --s fsaverage'.format(full=filelist[0], base=base)
```

### Step 3: Assign bbr.inputs.subject_id = 'fsaverage'

```python
bbr.inputs.subject_id = 'fsaverage'
```

### Step 4: Assign bbr.inputs.source_file = value

```python
bbr.inputs.source_file = filelist[0]
```

### Step 5: Assign bbr.inputs.contrast_type = 't2'

```python
bbr.inputs.contrast_type = 't2'
```

### Step 6: Assign bbr.inputs.init = 'fsl'

```python
bbr.inputs.init = 'fsl'
```

### Step 7: Assign unknown = os.path.splitext(...)

```python
base, ext = os.path.splitext(os.path.basename(filelist[0]))
```

**Verification:**
```python
assert bbr.cmdline == 'bbregister --t2 --init-fsl --reg {base}_bbreg_fsaverage.dat --mov {full} --s fsaverage'.format(full=filelist[0], base=base)
```

### Step 8: bbr.cmdline

```python
bbr.cmdline
```

### Step 9: bbr.cmdline

```python
bbr.cmdline
```

### Step 10: Assign unknown = os.path.splitext(...)

```python
base, _ = os.path.splitext(base)
```

### Step 11: bbr.cmdline

```python
bbr.cmdline
```


## Complete Example

```python
# Setup
# Fixtures: create_files_in_directory

# Workflow
filelist, outdir = create_files_in_directory
bbr = freesurfer.BBRegister()
assert bbr.cmd == 'bbregister'
with pytest.raises(ValueError):
    bbr.cmdline
bbr.inputs.subject_id = 'fsaverage'
bbr.inputs.source_file = filelist[0]
bbr.inputs.contrast_type = 't2'
if Info.looseversion() < LooseVersion('6.0.0'):
    with pytest.raises(ValueError):
        bbr.cmdline
else:
    bbr.cmdline
bbr.inputs.init = 'fsl'
base, ext = os.path.splitext(os.path.basename(filelist[0]))
if ext == '.gz':
    base, _ = os.path.splitext(base)
assert bbr.cmdline == 'bbregister --t2 --init-fsl --reg {base}_bbreg_fsaverage.dat --mov {full} --s fsaverage'.format(full=filelist[0], base=base)
```

## Next Steps


---

*Source: test_preprocess.py:158 | Complexity: Advanced | Last updated: 2026-05-18*