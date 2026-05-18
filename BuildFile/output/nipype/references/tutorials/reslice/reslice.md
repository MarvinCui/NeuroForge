# How To: Reslice

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test reslice

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
assert reslice.inputs.matlab_cmd == 'mymatlab_version'
```

### Step 2: Assign space_defining = example_data(...)

```python
space_defining = example_data(infile='T1.nii')
```

**Verification:**
```python
assert reslice.inputs.interp == 0
```

### Step 3: Assign reslice = spmu.Reslice(...)

```python
reslice = spmu.Reslice(matlab_cmd='mymatlab_version')
```

**Verification:**
```python
assert reslice.inputs.out_file == outfile
```

### Step 4: Assign reslice.inputs.in_file = moving

```python
reslice.inputs.in_file = moving
```

**Verification:**
```python
assert expected in script.replace(' ', '')
```

### Step 5: Assign reslice.inputs.space_defining = space_defining

```python
reslice.inputs.space_defining = space_defining
```

**Verification:**
```python
assert expected_interp in script
```

### Step 6: Assign reslice.inputs.interp = 1

```python
reslice.inputs.interp = 1
```

**Verification:**
```python
assert 'spm_reslice(invols, flags);' in script
```

### Step 7: Assign script = reslice._make_matlab_command(...)

```python
script = reslice._make_matlab_command(None)
```

### Step 8: Assign outfile = fname_presuffix(...)

```python
outfile = fname_presuffix(moving, prefix='r')
```

**Verification:**
```python
assert reslice.inputs.out_file == outfile
```

### Step 9: Assign expected = '\nflags.mean=0;\nflags.which=1;\nflags.mask=0;'

```python
expected = '\nflags.mean=0;\nflags.which=1;\nflags.mask=0;'
```

**Verification:**
```python
assert expected in script.replace(' ', '')
```

### Step 10: Assign expected_interp = 'flags.interp = 1;\n'

```python
expected_interp = 'flags.interp = 1;\n'
```

**Verification:**
```python
assert expected_interp in script
```

### Step 11: Call reslice.inputs.trait_set()

```python
reslice.inputs.trait_set(interp='nearest')
```

### Step 12: Call reslice.inputs.trait_set()

```python
reslice.inputs.trait_set(interp=10)
```


## Complete Example

```python
# Workflow
moving = example_data(infile='functional.nii')
space_defining = example_data(infile='T1.nii')
reslice = spmu.Reslice(matlab_cmd='mymatlab_version')
assert reslice.inputs.matlab_cmd == 'mymatlab_version'
reslice.inputs.in_file = moving
reslice.inputs.space_defining = space_defining
assert reslice.inputs.interp == 0
with pytest.raises(TraitError):
    reslice.inputs.trait_set(interp='nearest')
with pytest.raises(TraitError):
    reslice.inputs.trait_set(interp=10)
reslice.inputs.interp = 1
script = reslice._make_matlab_command(None)
outfile = fname_presuffix(moving, prefix='r')
assert reslice.inputs.out_file == outfile
expected = '\nflags.mean=0;\nflags.which=1;\nflags.mask=0;'
assert expected in script.replace(' ', '')
expected_interp = 'flags.interp = 1;\n'
assert expected_interp in script
assert 'spm_reslice(invols, flags);' in script
```

## Next Steps


---

*Source: test_utils.py:44 | Complexity: Advanced | Last updated: 2026-05-18*