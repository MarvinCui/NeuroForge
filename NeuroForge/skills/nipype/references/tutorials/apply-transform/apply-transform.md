# How To: Apply Transform

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test apply transform

## Prerequisites

**Required Modules:**
- `os`
- `pytest`
- `nipype.testing`
- `nipype.interfaces.spm.utils`
- `nipype.interfaces.base`
- `nipype.utils.filemanip`
- `nipype.interfaces.base`


## Step-by-Step Guide

### Step 1: Assign moving = example_data(...)

```python
moving = example_data(infile='functional.nii')
```

**Verification:**
```python
assert applymat.inputs.matlab_cmd == 'mymatlab'
```

### Step 2: Assign mat = example_data(...)

```python
mat = example_data(infile='trans.mat')
```

**Verification:**
```python
assert expected in script
```

### Step 3: Assign applymat = spmu.ApplyTransform(...)

```python
applymat = spmu.ApplyTransform(matlab_cmd='mymatlab')
```

**Verification:**
```python
assert expected in script
```

### Step 4: Assign applymat.inputs.in_file = moving

```python
applymat.inputs.in_file = moving
```

### Step 5: Assign applymat.inputs.mat = mat

```python
applymat.inputs.mat = mat
```

### Step 6: Assign script = applymat._make_matlab_command(...)

```python
script = applymat._make_matlab_command(None)
```

### Step 7: Assign expected = '[p n e v] = spm_fileparts(V.fname);'

```python
expected = '[p n e v] = spm_fileparts(V.fname);'
```

**Verification:**
```python
assert expected in script
```

### Step 8: Assign expected = 'V.mat = transform.M * V.mat;'

```python
expected = 'V.mat = transform.M * V.mat;'
```

**Verification:**
```python
assert expected in script
```


## Complete Example

```python
# Workflow
moving = example_data(infile='functional.nii')
mat = example_data(infile='trans.mat')
applymat = spmu.ApplyTransform(matlab_cmd='mymatlab')
assert applymat.inputs.matlab_cmd == 'mymatlab'
applymat.inputs.in_file = moving
applymat.inputs.mat = mat
script = applymat._make_matlab_command(None)
expected = '[p n e v] = spm_fileparts(V.fname);'
assert expected in script
expected = 'V.mat = transform.M * V.mat;'
assert expected in script
```

## Next Steps


---

*Source: test_utils.py:30 | Complexity: Advanced | Last updated: 2026-05-18*