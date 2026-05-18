# How To: Convertxfm

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test convertxfm

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
assert cvt.cmd == 'convert_xfm'
```

### Step 2: Assign cvt = fsl.ConvertXFM(...)

```python
cvt = fsl.ConvertXFM()
```

**Verification:**
```python
assert cvt.cmdline == 'convert_xfm -omat foo.mat -inverse %s' % filelist[0]
```

### Step 3: Assign cvt.inputs.in_file = value

```python
cvt.inputs.in_file = filelist[0]
```

**Verification:**
```python
assert cvt2.cmdline == 'convert_xfm -omat bar.mat -concat {} {}'.format(filelist[1], filelist[0])
```

### Step 4: Assign cvt.inputs.invert_xfm = True

```python
cvt.inputs.invert_xfm = True
```

### Step 5: Assign cvt.inputs.out_file = 'foo.mat'

```python
cvt.inputs.out_file = 'foo.mat'
```

**Verification:**
```python
assert cvt.cmdline == 'convert_xfm -omat foo.mat -inverse %s' % filelist[0]
```

### Step 6: Assign cvt2 = fsl.ConvertXFM(...)

```python
cvt2 = fsl.ConvertXFM(in_file=filelist[0], in_file2=filelist[1], concat_xfm=True, out_file='bar.mat')
```

**Verification:**
```python
assert cvt2.cmdline == 'convert_xfm -omat bar.mat -concat {} {}'.format(filelist[1], filelist[0])
```

### Step 7: Call cvt.run()

```python
cvt.run()
```


## Complete Example

```python
# Setup
# Fixtures: create_files_in_directory_plus_output_type

# Workflow
filelist, outdir, _ = create_files_in_directory_plus_output_type
cvt = fsl.ConvertXFM()
assert cvt.cmd == 'convert_xfm'
with pytest.raises(ValueError):
    cvt.run()
cvt.inputs.in_file = filelist[0]
cvt.inputs.invert_xfm = True
cvt.inputs.out_file = 'foo.mat'
assert cvt.cmdline == 'convert_xfm -omat foo.mat -inverse %s' % filelist[0]
cvt2 = fsl.ConvertXFM(in_file=filelist[0], in_file2=filelist[1], concat_xfm=True, out_file='bar.mat')
assert cvt2.cmdline == 'convert_xfm -omat bar.mat -concat {} {}'.format(filelist[1], filelist[0])
```

## Next Steps


---

*Source: test_utils.py:299 | Complexity: Intermediate | Last updated: 2026-05-18*