# How To: Synthstrip Interface

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test qsiprep.interfaces.freesurfer.FixHeaderSynthStrip.

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

### Step 1: 'Test qsiprep.interfaces.freesurfer.FixHeaderSynthStrip.'

```python
'Test qsiprep.interfaces.freesurfer.FixHeaderSynthStrip.'
```

**Verification:**
```python
assert os.path.isfile(results.outputs.out_brain)
```

### Step 2: Assign tmpdir = tmp_path_factory.mktemp(...)

```python
tmpdir = tmp_path_factory.mktemp('test_synthstrip')
```

**Verification:**
```python
assert os.path.isfile(results.outputs.out_brain_mask)
```

### Step 3: Assign in_file = _resample_to_64_cube(...)

```python
in_file = _resample_to_64_cube(_get_forrest_gump_t1w(datasets), tmpdir)
```

**Verification:**
```python
assert out_img.shape == in_img.shape
```

### Step 4: Assign in_img = nb.load(...)

```python
in_img = nb.load(in_file)
```

**Verification:**
```python
assert mask_img.shape == in_img.shape
```

### Step 5: Assign use_gpu = _gpu_available(...)

```python
use_gpu = _gpu_available()
```

### Step 6: Assign interface = freesurfer.FixHeaderSynthStrip(...)

```python
interface = freesurfer.FixHeaderSynthStrip(input_image=in_file, gpu=use_gpu)
```

### Step 7: Assign results = interface.run(...)

```python
results = interface.run(cwd=tmpdir)
```

**Verification:**
```python
assert os.path.isfile(results.outputs.out_brain)
```

### Step 8: Assign out_img = nb.load(...)

```python
out_img = nb.load(results.outputs.out_brain)
```

### Step 9: Assign mask_img = nb.load(...)

```python
mask_img = nb.load(results.outputs.out_brain_mask)
```

**Verification:**
```python
assert out_img.shape == in_img.shape
```


## Complete Example

```python
# Setup
# Fixtures: datasets, tmp_path_factory

# Workflow
'Test qsiprep.interfaces.freesurfer.FixHeaderSynthStrip.'
tmpdir = tmp_path_factory.mktemp('test_synthstrip')
in_file = _resample_to_64_cube(_get_forrest_gump_t1w(datasets), tmpdir)
in_img = nb.load(in_file)
use_gpu = _gpu_available()
interface = freesurfer.FixHeaderSynthStrip(input_image=in_file, gpu=use_gpu)
results = interface.run(cwd=tmpdir)
assert os.path.isfile(results.outputs.out_brain)
assert os.path.isfile(results.outputs.out_brain_mask)
out_img = nb.load(results.outputs.out_brain)
mask_img = nb.load(results.outputs.out_brain_mask)
assert out_img.shape == in_img.shape
assert mask_img.shape == in_img.shape
```

## Next Steps


---

*Source: test_interfaces_freesurfer.py:48 | Complexity: Advanced | Last updated: 2026-05-18*