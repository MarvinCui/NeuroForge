# How To: Robustregister

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test robustregister

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
assert reg.cmd == 'mri_robust_register'
```

### Step 2: Assign reg = freesurfer.RobustRegister(...)

```python
reg = freesurfer.RobustRegister()
```

**Verification:**
```python
assert reg.cmdline == 'mri_robust_register --satit --lta %s/%s_robustreg.lta --mov %s --dst %s' % (cwd, filelist[0][:-4], filelist[0], filelist[1])
```

### Step 3: Assign cwd = os.getcwd(...)

```python
cwd = os.getcwd()
```

**Verification:**
```python
assert reg2.cmdline == 'mri_robust_register --halfdst %s_halfway.nii --lta foo.lta --sat 3.0000 --mov %s --dst %s' % (os.path.join(outdir, filelist[1][:-4]), filelist[0], filelist[1])
```

### Step 4: Assign reg.inputs.source_file = value

```python
reg.inputs.source_file = filelist[0]
```

### Step 5: Assign reg.inputs.target_file = value

```python
reg.inputs.target_file = filelist[1]
```

### Step 6: Assign reg.inputs.auto_sens = True

```python
reg.inputs.auto_sens = True
```

**Verification:**
```python
assert reg.cmdline == 'mri_robust_register --satit --lta %s/%s_robustreg.lta --mov %s --dst %s' % (cwd, filelist[0][:-4], filelist[0], filelist[1])
```

### Step 7: Assign reg2 = freesurfer.RobustRegister(...)

```python
reg2 = freesurfer.RobustRegister(source_file=filelist[0], target_file=filelist[1], outlier_sens=3.0, out_reg_file='foo.lta', half_targ=True)
```

**Verification:**
```python
assert reg2.cmdline == 'mri_robust_register --halfdst %s_halfway.nii --lta foo.lta --sat 3.0000 --mov %s --dst %s' % (os.path.join(outdir, filelist[1][:-4]), filelist[0], filelist[1])
```

### Step 8: Call reg.run()

```python
reg.run()
```


## Complete Example

```python
# Setup
# Fixtures: create_files_in_directory

# Workflow
filelist, outdir = create_files_in_directory
reg = freesurfer.RobustRegister()
cwd = os.getcwd()
assert reg.cmd == 'mri_robust_register'
with pytest.raises(ValueError):
    reg.run()
reg.inputs.source_file = filelist[0]
reg.inputs.target_file = filelist[1]
reg.inputs.auto_sens = True
assert reg.cmdline == 'mri_robust_register --satit --lta %s/%s_robustreg.lta --mov %s --dst %s' % (cwd, filelist[0][:-4], filelist[0], filelist[1])
reg2 = freesurfer.RobustRegister(source_file=filelist[0], target_file=filelist[1], outlier_sens=3.0, out_reg_file='foo.lta', half_targ=True)
assert reg2.cmdline == 'mri_robust_register --halfdst %s_halfway.nii --lta foo.lta --sat 3.0000 --mov %s --dst %s' % (os.path.join(outdir, filelist[1][:-4]), filelist[0], filelist[1])
```

## Next Steps


---

*Source: test_preprocess.py:14 | Complexity: Advanced | Last updated: 2026-05-18*