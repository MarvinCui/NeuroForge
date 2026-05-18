# How To: Synthseg Interface

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test qsiprep.interfaces.freesurfer.SynthSeg.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `shutil`
- `nibabel`
- `numpy`
- `pytest`
- `nibabel.processing`
- `qsiprep.interfaces`

**Setup Required:**
```python
# Fixtures: datasets, tmp_path_factory
```

## Step-by-Step Guide

### Step 1: 'Test qsiprep.interfaces.freesurfer.SynthSeg.'

```python
'Test qsiprep.interfaces.freesurfer.SynthSeg.'
```

**Verification:**
```python
assert os.path.isfile(results.outputs.out_seg)
```

### Step 2: Assign tmpdir = tmp_path_factory.mktemp(...)

```python
tmpdir = tmp_path_factory.mktemp('test_synthseg')
```

**Verification:**
```python
assert os.path.isfile(results.outputs.out_post)
```

### Step 3: Assign in_file = _resample_to_64_cube(...)

```python
in_file = _resample_to_64_cube(_get_forrest_gump_t1w(datasets), tmpdir)
```

**Verification:**
```python
assert os.path.isfile(results.outputs.out_qc)
```

### Step 4: Assign use_gpu = _gpu_available(...)

```python
use_gpu = _gpu_available()
```

**Verification:**
```python
assert seg_img.shape == post_img.shape[:3]
```

### Step 5: Assign interface = freesurfer.SynthSeg(...)

```python
interface = freesurfer.SynthSeg(input_image=in_file, cpu=not use_gpu)
```

### Step 6: Assign results = interface.run(...)

```python
results = interface.run(cwd=tmpdir)
```

**Verification:**
```python
assert os.path.isfile(results.outputs.out_seg)
```

### Step 7: Assign seg_img = nb.load(...)

```python
seg_img = nb.load(results.outputs.out_seg)
```

### Step 8: Assign post_img = nb.load(...)

```python
post_img = nb.load(results.outputs.out_post)
```

**Verification:**
```python
assert seg_img.shape == post_img.shape[:3]
```


## Complete Example

```python
# Setup
# Fixtures: datasets, tmp_path_factory

# Workflow
'Test qsiprep.interfaces.freesurfer.SynthSeg.'
tmpdir = tmp_path_factory.mktemp('test_synthseg')
in_file = _resample_to_64_cube(_get_forrest_gump_t1w(datasets), tmpdir)
use_gpu = _gpu_available()
interface = freesurfer.SynthSeg(input_image=in_file, cpu=not use_gpu)
results = interface.run(cwd=tmpdir)
assert os.path.isfile(results.outputs.out_seg)
assert os.path.isfile(results.outputs.out_post)
assert os.path.isfile(results.outputs.out_qc)
seg_img = nb.load(results.outputs.out_seg)
post_img = nb.load(results.outputs.out_post)
assert seg_img.shape == post_img.shape[:3]
```

## Next Steps


---

*Source: test_interfaces_freesurfer.py:68 | Complexity: Advanced | Last updated: 2026-05-18*