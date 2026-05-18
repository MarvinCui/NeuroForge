# How To: Synthesizeflash

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test synthesizeflash

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
assert syn.cmd == 'mri_synthesize'
```

### Step 2: Assign syn = freesurfer.SynthesizeFLASH(...)

```python
syn = freesurfer.SynthesizeFLASH()
```

**Verification:**
```python
assert syn.cmdline == 'mri_synthesize 20.00 30.00 4.500 %s %s %s' % (filelist[0], filelist[1], os.path.join(outdir, 'synth-flash_30.mgz'))
```

### Step 3: Assign syn.inputs.t1_image = value

```python
syn.inputs.t1_image = filelist[0]
```

**Verification:**
```python
assert syn2.cmdline == 'mri_synthesize 25.00 20.00 5.000 %s %s %s' % (filelist[0], filelist[1], os.path.join(outdir, 'synth-flash_20.mgz'))
```

### Step 4: Assign syn.inputs.pd_image = value

```python
syn.inputs.pd_image = filelist[1]
```

### Step 5: Assign syn.inputs.flip_angle = 30

```python
syn.inputs.flip_angle = 30
```

### Step 6: Assign syn.inputs.te = 4.5

```python
syn.inputs.te = 4.5
```

### Step 7: Assign syn.inputs.tr = 20

```python
syn.inputs.tr = 20
```

**Verification:**
```python
assert syn.cmdline == 'mri_synthesize 20.00 30.00 4.500 %s %s %s' % (filelist[0], filelist[1], os.path.join(outdir, 'synth-flash_30.mgz'))
```

### Step 8: Assign syn2 = freesurfer.SynthesizeFLASH(...)

```python
syn2 = freesurfer.SynthesizeFLASH(t1_image=filelist[0], pd_image=filelist[1], flip_angle=20, te=5, tr=25)
```

**Verification:**
```python
assert syn2.cmdline == 'mri_synthesize 25.00 20.00 5.000 %s %s %s' % (filelist[0], filelist[1], os.path.join(outdir, 'synth-flash_20.mgz'))
```

### Step 9: Call syn.run()

```python
syn.run()
```


## Complete Example

```python
# Setup
# Fixtures: create_files_in_directory

# Workflow
filelist, outdir = create_files_in_directory
syn = freesurfer.SynthesizeFLASH()
assert syn.cmd == 'mri_synthesize'
with pytest.raises(ValueError):
    syn.run()
syn.inputs.t1_image = filelist[0]
syn.inputs.pd_image = filelist[1]
syn.inputs.flip_angle = 30
syn.inputs.te = 4.5
syn.inputs.tr = 20
assert syn.cmdline == 'mri_synthesize 20.00 30.00 4.500 %s %s %s' % (filelist[0], filelist[1], os.path.join(outdir, 'synth-flash_30.mgz'))
syn2 = freesurfer.SynthesizeFLASH(t1_image=filelist[0], pd_image=filelist[1], flip_angle=20, te=5, tr=25)
assert syn2.cmdline == 'mri_synthesize 25.00 20.00 5.000 %s %s %s' % (filelist[0], filelist[1], os.path.join(outdir, 'synth-flash_20.mgz'))
```

## Next Steps


---

*Source: test_preprocess.py:85 | Complexity: Advanced | Last updated: 2026-05-18*