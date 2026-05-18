# How To: Overlay

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test overlay

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `numpy`
- `pytest`
- `nipype.interfaces.fsl.utils`
- `nipype.interfaces.fsl`
- `nipype.testing.fixtures`

**Setup Required:**
```python
# Fixtures: create_files_in_directory_plus_output_type
```

## Step-by-Step Guide

### Step 1: Assign unknown = create_files_in_directory_plus_output_type

```python
filelist, outdir, _ = create_files_in_directory_plus_output_type
```

**Verification:**
```python
assert overlay.cmd == 'overlay'
```

### Step 2: Assign overlay = fsl.Overlay(...)

```python
overlay = fsl.Overlay()
```

**Verification:**
```python
assert overlay.cmdline == 'overlay 1 0 %s -a %s 2.50 10.00 %s -2.50 -10.00 foo_overlay.nii' % (filelist[1], filelist[0], filelist[0])
```

### Step 3: Assign overlay.inputs.stat_image = value

```python
overlay.inputs.stat_image = filelist[0]
```

**Verification:**
```python
assert overlay2.cmdline == 'overlay 1 0 {} -a {} 2.50 10.00 foo2_overlay.nii'.format(filelist[1], filelist[0])
```

### Step 4: Assign overlay.inputs.stat_thresh = value

```python
overlay.inputs.stat_thresh = (2.5, 10)
```

### Step 5: Assign overlay.inputs.background_image = value

```python
overlay.inputs.background_image = filelist[1]
```

### Step 6: Assign overlay.inputs.auto_thresh_bg = True

```python
overlay.inputs.auto_thresh_bg = True
```

### Step 7: Assign overlay.inputs.show_negative_stats = True

```python
overlay.inputs.show_negative_stats = True
```

### Step 8: Assign overlay.inputs.out_file = 'foo_overlay.nii'

```python
overlay.inputs.out_file = 'foo_overlay.nii'
```

**Verification:**
```python
assert overlay.cmdline == 'overlay 1 0 %s -a %s 2.50 10.00 %s -2.50 -10.00 foo_overlay.nii' % (filelist[1], filelist[0], filelist[0])
```

### Step 9: Assign overlay2 = fsl.Overlay(...)

```python
overlay2 = fsl.Overlay(stat_image=filelist[0], stat_thresh=(2.5, 10), background_image=filelist[1], auto_thresh_bg=True, out_file='foo2_overlay.nii')
```

**Verification:**
```python
assert overlay2.cmdline == 'overlay 1 0 {} -a {} 2.50 10.00 foo2_overlay.nii'.format(filelist[1], filelist[0])
```

### Step 10: Call overlay.run()

```python
overlay.run()
```


## Complete Example

```python
# Setup
# Fixtures: create_files_in_directory_plus_output_type

# Workflow
filelist, outdir, _ = create_files_in_directory_plus_output_type
overlay = fsl.Overlay()
assert overlay.cmd == 'overlay'
with pytest.raises(ValueError):
    overlay.run()
overlay.inputs.stat_image = filelist[0]
overlay.inputs.stat_thresh = (2.5, 10)
overlay.inputs.background_image = filelist[1]
overlay.inputs.auto_thresh_bg = True
overlay.inputs.show_negative_stats = True
overlay.inputs.out_file = 'foo_overlay.nii'
assert overlay.cmdline == 'overlay 1 0 %s -a %s 2.50 10.00 %s -2.50 -10.00 foo_overlay.nii' % (filelist[1], filelist[0], filelist[0])
overlay2 = fsl.Overlay(stat_image=filelist[0], stat_thresh=(2.5, 10), background_image=filelist[1], auto_thresh_bg=True, out_file='foo2_overlay.nii')
assert overlay2.cmdline == 'overlay 1 0 {} -a {} 2.50 10.00 foo2_overlay.nii'.format(filelist[1], filelist[0])
```

## Next Steps


---

*Source: test_utils.py:137 | Complexity: Advanced | Last updated: 2026-05-18*