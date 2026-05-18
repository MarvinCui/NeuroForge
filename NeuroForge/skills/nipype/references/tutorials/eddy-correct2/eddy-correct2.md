# How To: Eddy Correct2

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test eddy correct2

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pytest`
- `nipype.testing.fixtures`
- `nipype.interfaces.fsl.epi`
- `nipype.interfaces.fsl`

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
assert eddy.cmd == 'eddy_correct'
```

### Step 2: Assign eddy = fsl.EddyCorrect(...)

```python
eddy = fsl.EddyCorrect()
```

**Verification:**
```python
assert eddy.cmdline == 'eddy_correct %s foo_eddc.nii 100' % filelist[0]
```

### Step 3: Assign eddy.inputs.in_file = value

```python
eddy.inputs.in_file = filelist[0]
```

**Verification:**
```python
assert eddy2.cmdline == 'eddy_correct %s foo_ec.nii 20' % filelist[0]
```

### Step 4: Assign eddy.inputs.out_file = 'foo_eddc.nii'

```python
eddy.inputs.out_file = 'foo_eddc.nii'
```

### Step 5: Assign eddy.inputs.ref_num = 100

```python
eddy.inputs.ref_num = 100
```

**Verification:**
```python
assert eddy.cmdline == 'eddy_correct %s foo_eddc.nii 100' % filelist[0]
```

### Step 6: Assign eddy2 = fsl.EddyCorrect(...)

```python
eddy2 = fsl.EddyCorrect(in_file=filelist[0], out_file='foo_ec.nii', ref_num=20)
```

**Verification:**
```python
assert eddy2.cmdline == 'eddy_correct %s foo_ec.nii 20' % filelist[0]
```

### Step 7: Call eddy.run()

```python
eddy.run()
```


## Complete Example

```python
# Setup
# Fixtures: create_files_in_directory

# Workflow
filelist, outdir = create_files_in_directory
eddy = fsl.EddyCorrect()
assert eddy.cmd == 'eddy_correct'
with pytest.raises(ValueError):
    eddy.run()
eddy.inputs.in_file = filelist[0]
eddy.inputs.out_file = 'foo_eddc.nii'
eddy.inputs.ref_num = 100
assert eddy.cmdline == 'eddy_correct %s foo_eddc.nii 100' % filelist[0]
eddy2 = fsl.EddyCorrect(in_file=filelist[0], out_file='foo_ec.nii', ref_num=20)
assert eddy2.cmdline == 'eddy_correct %s foo_ec.nii 20' % filelist[0]
```

## Next Steps


---

*Source: test_epi.py:13 | Complexity: Intermediate | Last updated: 2026-05-18*