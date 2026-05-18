# How To: Coreg

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test coreg

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
assert coreg.inputs.matlab_cmd == 'mymatlab'
```

### Step 2: Assign target = example_data(...)

```python
target = example_data(infile='T1.nii')
```

**Verification:**
```python
assert not isdefined(coreg.inputs.mat)
```

### Step 3: Assign mat = example_data(...)

```python
mat = example_data(infile='trans.mat')
```

**Verification:**
```python
assert coreg.inputs.mat == mat
```

### Step 4: Assign coreg = spmu.CalcCoregAffine(...)

```python
coreg = spmu.CalcCoregAffine(matlab_cmd='mymatlab')
```

**Verification:**
```python
assert coreg.inputs.invmat == invmat
```

### Step 5: Assign coreg.inputs.target = target

```python
coreg.inputs.target = target
```

**Verification:**
```python
assert coreg.inputs.matlab_cmd == 'mymatlab'
```

### Step 6: Assign coreg.inputs.moving = moving

```python
coreg.inputs.moving = moving
```

**Verification:**
```python
assert not isdefined(coreg.inputs.mat)
```

### Step 7: Assign unknown = split_filename(...)

```python
pth, mov, _ = split_filename(moving)
```

### Step 8: Assign unknown = split_filename(...)

```python
_, tgt, _ = split_filename(target)
```

### Step 9: Assign mat = os.path.join(...)

```python
mat = os.path.join(pth, f'{mov}_to_{tgt}.mat')
```

### Step 10: Assign invmat = fname_presuffix(...)

```python
invmat = fname_presuffix(mat, prefix='inverse_')
```

### Step 11: Assign script = coreg._make_matlab_command(...)

```python
script = coreg._make_matlab_command(None)
```

**Verification:**
```python
assert coreg.inputs.mat == mat
```


## Complete Example

```python
# Workflow
moving = example_data(infile='functional.nii')
target = example_data(infile='T1.nii')
mat = example_data(infile='trans.mat')
coreg = spmu.CalcCoregAffine(matlab_cmd='mymatlab')
coreg.inputs.target = target
assert coreg.inputs.matlab_cmd == 'mymatlab'
coreg.inputs.moving = moving
assert not isdefined(coreg.inputs.mat)
pth, mov, _ = split_filename(moving)
_, tgt, _ = split_filename(target)
mat = os.path.join(pth, f'{mov}_to_{tgt}.mat')
invmat = fname_presuffix(mat, prefix='inverse_')
script = coreg._make_matlab_command(None)
assert coreg.inputs.mat == mat
assert coreg.inputs.invmat == invmat
```

## Next Steps


---

*Source: test_utils.py:12 | Complexity: Advanced | Last updated: 2026-05-18*