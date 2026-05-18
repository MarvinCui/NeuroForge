# How To: Namesource Constraints

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test namesource constraints

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `warnings`
- `pytest`
- `utils.filemanip`
- `base`
- `interfaces`
- `utility.wrappers`
- `pipeline`
- `specs`
- `pickle`

**Setup Required:**
```python
# Fixtures: setup_file
```

## Step-by-Step Guide

### Step 1: Assign tmp_infile = setup_file

```python
tmp_infile = setup_file
```

**Verification:**
```python
assert tc.cmdline == 'mycommand'
```

### Step 2: Assign unknown = split_filename(...)

```python
tmpd, nme, ext = split_filename(tmp_infile)
```

**Verification:**
```python
assert tc.cmdline == 'mycommand foo.txt foo_mask.txt foo_out1.txt'
```

### Step 3: Assign tc = TestConstrained(...)

```python
tc = TestConstrained()
```

**Verification:**
```python
assert tc.cmdline == 'mycommand foo.txt 10 foo_out1.txt foo_out2.txt'
```

### Step 4: Assign tc.inputs.in_file = os.path.basename(...)

```python
tc.inputs.in_file = os.path.basename(tmp_infile)
```

**Verification:**
```python
assert tc.cmdline == 'mycommand foo.txt foo_mask.txt foo_out1.txt'
```

### Step 5: Assign tc.inputs.threshold = 10.0

```python
tc.inputs.threshold = 10.0
```

**Verification:**
```python
assert tc.cmdline == 'mycommand foo.txt 10 foo_out1.txt foo_out2.txt'
```

### Step 6: Assign in_file = nib.File(...)

```python
in_file = nib.File(argstr='%s', position=1)
```

### Step 7: Assign threshold = traits.Float(...)

```python
threshold = traits.Float(argstr='%g', xor=['mask_file'], position=2)
```

### Step 8: Assign mask_file = nib.File(...)

```python
mask_file = nib.File(argstr='%s', name_source=['in_file'], name_template='%s_mask', keep_extension=True, xor=['threshold'], position=2)
```

### Step 9: Assign out_file1 = nib.File(...)

```python
out_file1 = nib.File(argstr='%s', name_source=['in_file'], name_template='%s_out1', keep_extension=True, position=3)
```

### Step 10: Assign out_file2 = nib.File(...)

```python
out_file2 = nib.File(argstr='%s', name_source=['in_file'], name_template='%s_out2', keep_extension=True, requires=['threshold'], position=4)
```

### Step 11: Assign _cmd = 'mycommand'

```python
_cmd = 'mycommand'
```

### Step 12: Assign input_spec = constrained_spec

```python
input_spec = constrained_spec
```


## Complete Example

```python
# Setup
# Fixtures: setup_file

# Workflow
tmp_infile = setup_file
tmpd, nme, ext = split_filename(tmp_infile)

class constrained_spec(nib.CommandLineInputSpec):
    in_file = nib.File(argstr='%s', position=1)
    threshold = traits.Float(argstr='%g', xor=['mask_file'], position=2)
    mask_file = nib.File(argstr='%s', name_source=['in_file'], name_template='%s_mask', keep_extension=True, xor=['threshold'], position=2)
    out_file1 = nib.File(argstr='%s', name_source=['in_file'], name_template='%s_out1', keep_extension=True, position=3)
    out_file2 = nib.File(argstr='%s', name_source=['in_file'], name_template='%s_out2', keep_extension=True, requires=['threshold'], position=4)

class TestConstrained(nib.CommandLine):
    _cmd = 'mycommand'
    input_spec = constrained_spec
tc = TestConstrained()
assert tc.cmdline == 'mycommand'
tc.inputs.in_file = os.path.basename(tmp_infile)
assert tc.cmdline == 'mycommand foo.txt foo_mask.txt foo_out1.txt'
tc.inputs.threshold = 10.0
assert tc.cmdline == 'mycommand foo.txt 10 foo_out1.txt foo_out2.txt'
```

## Next Steps


---

*Source: test_specs.py:321 | Complexity: Advanced | Last updated: 2026-05-18*