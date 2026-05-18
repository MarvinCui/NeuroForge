# How To: Dwidenoise

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test qsiprep.interfaces.mrtrix.DWIDenoise.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `nibabel`
- `qsiprep.interfaces`

**Setup Required:**
```python
# Fixtures: datasets, tmp_path_factory
```

## Step-by-Step Guide

### Step 1: 'Test qsiprep.interfaces.mrtrix.DWIDenoise.'

```python
'Test qsiprep.interfaces.mrtrix.DWIDenoise.'
```

**Verification:**
```python
assert os.path.isfile(results.outputs.out_file)
```

### Step 2: Assign tmpdir = tmp_path_factory.mktemp(...)

```python
tmpdir = tmp_path_factory.mktemp('test_dwidenoise')
```

**Verification:**
```python
assert denoised_img.shape == in_img.shape
```

### Step 3: Assign in_dir = value

```python
in_dir = datasets['forrest_gump']
```

**Verification:**
```python
assert os.path.isfile(results.outputs.noise_image)
```

### Step 4: Assign in_file = os.path.join(...)

```python
in_file = os.path.join(in_dir, 'sub-01/ses-forrestgump/dwi/sub-01_ses-forrestgump_dwi.nii.gz')
```

**Verification:**
```python
assert noise_img.shape == in_img.shape[:3]
```

### Step 5: Assign in_img = nb.load(...)

```python
in_img = nb.load(in_file)
```

**Verification:**
```python
assert noise_img.ndim == 3
```

### Step 6: Assign interface = mrtrix.DWIDenoise(...)

```python
interface = mrtrix.DWIDenoise(extent=(5, 5, 5), in_file=in_file, nthreads=1)
```

**Verification:**
```python
assert os.path.isfile(results.outputs.out_report)
```

### Step 7: Assign results = interface.run(...)

```python
results = interface.run(cwd=tmpdir)
```

**Verification:**
```python
assert os.path.isfile(results.outputs.nmse_text)
```

### Step 8: Assign denoised_img = nb.load(...)

```python
denoised_img = nb.load(results.outputs.out_file)
```

**Verification:**
```python
assert denoised_img.shape == in_img.shape
```

### Step 9: Assign noise_img = nb.load(...)

```python
noise_img = nb.load(results.outputs.noise_image)
```

**Verification:**
```python
assert noise_img.shape == in_img.shape[:3]
```


## Complete Example

```python
# Setup
# Fixtures: datasets, tmp_path_factory

# Workflow
'Test qsiprep.interfaces.mrtrix.DWIDenoise.'
tmpdir = tmp_path_factory.mktemp('test_dwidenoise')
in_dir = datasets['forrest_gump']
in_file = os.path.join(in_dir, 'sub-01/ses-forrestgump/dwi/sub-01_ses-forrestgump_dwi.nii.gz')
in_img = nb.load(in_file)
interface = mrtrix.DWIDenoise(extent=(5, 5, 5), in_file=in_file, nthreads=1)
results = interface.run(cwd=tmpdir)
assert os.path.isfile(results.outputs.out_file)
denoised_img = nb.load(results.outputs.out_file)
assert denoised_img.shape == in_img.shape
assert os.path.isfile(results.outputs.noise_image)
noise_img = nb.load(results.outputs.noise_image)
assert noise_img.shape == in_img.shape[:3]
assert noise_img.ndim == 3
assert os.path.isfile(results.outputs.out_report)
assert os.path.isfile(results.outputs.nmse_text)
```

## Next Steps


---

*Source: test_interfaces_mrtrix3.py:10 | Complexity: Advanced | Last updated: 2026-05-18*