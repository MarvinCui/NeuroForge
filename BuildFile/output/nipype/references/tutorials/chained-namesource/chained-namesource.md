# How To: Chained Namesource

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test chained namesource

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
assert '%s' % tmp_infile in res
```

### Step 2: Assign unknown = split_filename(...)

```python
tmpd, nme, ext = split_filename(tmp_infile)
```

**Verification:**
```python
assert '%s_mootpl ' % nme in res
```

### Step 3: Assign testobj = TestName(...)

```python
testobj = TestName()
```

**Verification:**
```python
assert '%s_mootpl_generated' % nme in res
```

### Step 4: Assign testobj.inputs.doo = tmp_infile

```python
testobj.inputs.doo = tmp_infile
```

### Step 5: Assign res = value

```python
res = testobj.cmdline
```

**Verification:**
```python
assert '%s' % tmp_infile in res
```

### Step 6: Assign doo = nib.File(...)

```python
doo = nib.File(exists=True, argstr='%s', position=1)
```

### Step 7: Assign moo = nib.File(...)

```python
moo = nib.File(name_source=['doo'], hash_files=False, argstr='%s', position=2, name_template='%s_mootpl')
```

### Step 8: Assign poo = nib.File(...)

```python
poo = nib.File(name_source=['moo'], hash_files=False, argstr='%s', position=3)
```

### Step 9: Assign _cmd = 'mycommand'

```python
_cmd = 'mycommand'
```

### Step 10: Assign input_spec = spec2

```python
input_spec = spec2
```


## Complete Example

```python
# Setup
# Fixtures: setup_file

# Workflow
tmp_infile = setup_file
tmpd, nme, ext = split_filename(tmp_infile)

class spec2(nib.CommandLineInputSpec):
    doo = nib.File(exists=True, argstr='%s', position=1)
    moo = nib.File(name_source=['doo'], hash_files=False, argstr='%s', position=2, name_template='%s_mootpl')
    poo = nib.File(name_source=['moo'], hash_files=False, argstr='%s', position=3)

class TestName(nib.CommandLine):
    _cmd = 'mycommand'
    input_spec = spec2
testobj = TestName()
testobj.inputs.doo = tmp_infile
res = testobj.cmdline
assert '%s' % tmp_infile in res
assert '%s_mootpl ' % nme in res
assert '%s_mootpl_generated' % nme in res
```

## Next Steps


---

*Source: test_specs.py:229 | Complexity: Advanced | Last updated: 2026-05-18*