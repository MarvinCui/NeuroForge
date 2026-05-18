# How To: Namesource

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test namesource

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
assert '%s_generated' % nme in testobj.cmdline
```

### Step 2: Assign unknown = split_filename(...)

```python
tmpd, nme, ext = split_filename(tmp_infile)
```

**Verification:**
```python
assert '%d_generated' % testobj.inputs.goo in testobj.cmdline
```

### Step 3: Assign testobj = TestName(...)

```python
testobj = TestName()
```

**Verification:**
```python
assert 'my_%s_template' % nme in testobj.cmdline
```

### Step 4: Assign testobj.inputs.doo = tmp_infile

```python
testobj.inputs.doo = tmp_infile
```

### Step 5: Assign testobj.inputs.goo = 99

```python
testobj.inputs.goo = 99
```

**Verification:**
```python
assert '%s_generated' % nme in testobj.cmdline
```

### Step 6: Assign testobj.inputs.moo = 'my_%s_template'

```python
testobj.inputs.moo = 'my_%s_template'
```

**Verification:**
```python
assert 'my_%s_template' % nme in testobj.cmdline
```

### Step 7: Assign moo = nib.File(...)

```python
moo = nib.File(name_source=['doo'], hash_files=False, argstr='%s', position=2)
```

### Step 8: Assign doo = nib.File(...)

```python
doo = nib.File(exists=True, argstr='%s', position=1)
```

### Step 9: Assign goo = traits.Int(...)

```python
goo = traits.Int(argstr='%d', position=4)
```

### Step 10: Assign poo = nib.File(...)

```python
poo = nib.File(name_source=['goo'], hash_files=False, argstr='%s', position=3)
```

### Step 11: Assign _cmd = 'mycommand'

```python
_cmd = 'mycommand'
```

### Step 12: Assign input_spec = spec2

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
    moo = nib.File(name_source=['doo'], hash_files=False, argstr='%s', position=2)
    doo = nib.File(exists=True, argstr='%s', position=1)
    goo = traits.Int(argstr='%d', position=4)
    poo = nib.File(name_source=['goo'], hash_files=False, argstr='%s', position=3)

class TestName(nib.CommandLine):
    _cmd = 'mycommand'
    input_spec = spec2
testobj = TestName()
testobj.inputs.doo = tmp_infile
testobj.inputs.goo = 99
assert '%s_generated' % nme in testobj.cmdline
assert '%d_generated' % testobj.inputs.goo in testobj.cmdline
testobj.inputs.moo = 'my_%s_template'
assert 'my_%s_template' % nme in testobj.cmdline
```

## Next Steps


---

*Source: test_specs.py:206 | Complexity: Advanced | Last updated: 2026-05-18*