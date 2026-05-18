# How To: Slicer

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test slicer

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
assert slicer.cmd == 'slicer'
```

### Step 2: Assign slicer = fsl.Slicer(...)

```python
slicer = fsl.Slicer()
```

**Verification:**
```python
assert slicer.cmdline == 'slicer {} {} -L -i 10.000 20.000  -A 750 foo_bar.png'.format(filelist[0], filelist[1])
```

### Step 3: Assign slicer.inputs.in_file = value

```python
slicer.inputs.in_file = filelist[0]
```

**Verification:**
```python
assert slicer2.cmdline == 'slicer %s   -a foo_bar2.png' % filelist[0]
```

### Step 4: Assign slicer.inputs.image_edges = value

```python
slicer.inputs.image_edges = filelist[1]
```

### Step 5: Assign slicer.inputs.intensity_range = value

```python
slicer.inputs.intensity_range = (10.0, 20.0)
```

### Step 6: Assign slicer.inputs.all_axial = True

```python
slicer.inputs.all_axial = True
```

### Step 7: Assign slicer.inputs.image_width = 750

```python
slicer.inputs.image_width = 750
```

### Step 8: Assign slicer.inputs.out_file = 'foo_bar.png'

```python
slicer.inputs.out_file = 'foo_bar.png'
```

**Verification:**
```python
assert slicer.cmdline == 'slicer {} {} -L -i 10.000 20.000  -A 750 foo_bar.png'.format(filelist[0], filelist[1])
```

### Step 9: Assign slicer2 = fsl.Slicer(...)

```python
slicer2 = fsl.Slicer(in_file=filelist[0], middle_slices=True, label_slices=False, out_file='foo_bar2.png')
```

**Verification:**
```python
assert slicer2.cmdline == 'slicer %s   -a foo_bar2.png' % filelist[0]
```

### Step 10: Call slicer.run()

```python
slicer.run()
```


## Complete Example

```python
# Setup
# Fixtures: create_files_in_directory_plus_output_type

# Workflow
filelist, outdir, _ = create_files_in_directory_plus_output_type
slicer = fsl.Slicer()
assert slicer.cmd == 'slicer'
with pytest.raises(ValueError):
    slicer.run()
slicer.inputs.in_file = filelist[0]
slicer.inputs.image_edges = filelist[1]
slicer.inputs.intensity_range = (10.0, 20.0)
slicer.inputs.all_axial = True
slicer.inputs.image_width = 750
slicer.inputs.out_file = 'foo_bar.png'
assert slicer.cmdline == 'slicer {} {} -L -i 10.000 20.000  -A 750 foo_bar.png'.format(filelist[0], filelist[1])
slicer2 = fsl.Slicer(in_file=filelist[0], middle_slices=True, label_slices=False, out_file='foo_bar2.png')
assert slicer2.cmdline == 'slicer %s   -a foo_bar2.png' % filelist[0]
```

## Next Steps


---

*Source: test_utils.py:182 | Complexity: Advanced | Last updated: 2026-05-18*