# How To: Fitmsparams

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test fitmsparams

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
assert fit.cmd == 'mri_ms_fitparms'
```

### Step 2: Assign fit = freesurfer.FitMSParams(...)

```python
fit = freesurfer.FitMSParams()
```

**Verification:**
```python
assert fit.cmdline == 'mri_ms_fitparms  {} {} {}'.format(filelist[0], filelist[1], outdir)
```

### Step 3: Assign fit.inputs.in_files = filelist

```python
fit.inputs.in_files = filelist
```

**Verification:**
```python
assert fit2.cmdline == 'mri_ms_fitparms  -te %.3f -fa %.1f %s -te %.3f -fa %.1f %s %s' % (1.5, 20.0, filelist[0], 3.5, 30.0, filelist[1], outdir)
```

### Step 4: Assign fit.inputs.out_dir = outdir

```python
fit.inputs.out_dir = outdir
```

**Verification:**
```python
assert fit.cmdline == 'mri_ms_fitparms  {} {} {}'.format(filelist[0], filelist[1], outdir)
```

### Step 5: Assign fit2 = freesurfer.FitMSParams(...)

```python
fit2 = freesurfer.FitMSParams(in_files=filelist, te_list=[1.5, 3.5], flip_list=[20, 30], out_dir=outdir)
```

**Verification:**
```python
assert fit2.cmdline == 'mri_ms_fitparms  -te %.3f -fa %.1f %s -te %.3f -fa %.1f %s %s' % (1.5, 20.0, filelist[0], 3.5, 30.0, filelist[1], outdir)
```

### Step 6: Call fit.run()

```python
fit.run()
```


## Complete Example

```python
# Setup
# Fixtures: create_files_in_directory

# Workflow
filelist, outdir = create_files_in_directory
fit = freesurfer.FitMSParams()
assert fit.cmd == 'mri_ms_fitparms'
with pytest.raises(ValueError):
    fit.run()
fit.inputs.in_files = filelist
fit.inputs.out_dir = outdir
assert fit.cmdline == 'mri_ms_fitparms  {} {} {}'.format(filelist[0], filelist[1], outdir)
fit2 = freesurfer.FitMSParams(in_files=filelist, te_list=[1.5, 3.5], flip_list=[20, 30], out_dir=outdir)
assert fit2.cmdline == 'mri_ms_fitparms  -te %.3f -fa %.1f %s -te %.3f -fa %.1f %s %s' % (1.5, 20.0, filelist[0], 3.5, 30.0, filelist[1], outdir)
```

## Next Steps


---

*Source: test_preprocess.py:53 | Complexity: Intermediate | Last updated: 2026-05-18*