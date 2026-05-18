# How To: Cycle Namesource1

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test cycle namesource1

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
assert not not_raised
```

### Step 2: Assign unknown = split_filename(...)

```python
tmpd, nme, ext = split_filename(tmp_infile)
```

### Step 3: Assign to0 = TestCycle(...)

```python
to0 = TestCycle()
```

### Step 4: Assign not_raised = True

```python
not_raised = True
```

**Verification:**
```python
assert not not_raised
```

### Step 5: Assign moo = nib.File(...)

```python
moo = nib.File(name_source=['doo'], hash_files=False, argstr='%s', position=1, name_template='%s_mootpl')
```

### Step 6: Assign poo = nib.File(...)

```python
poo = nib.File(name_source=['moo'], hash_files=False, argstr='%s', position=2)
```

### Step 7: Assign doo = nib.File(...)

```python
doo = nib.File(name_source=['poo'], hash_files=False, argstr='%s', position=3)
```

### Step 8: Assign _cmd = 'mycommand'

```python
_cmd = 'mycommand'
```

### Step 9: Assign input_spec = spec3

```python
input_spec = spec3
```

### Step 10: to0.cmdline

```python
to0.cmdline
```

### Step 11: Assign not_raised = False

```python
not_raised = False
```


## Complete Example

```python
# Setup
# Fixtures: setup_file

# Workflow
tmp_infile = setup_file
tmpd, nme, ext = split_filename(tmp_infile)

class spec3(nib.CommandLineInputSpec):
    moo = nib.File(name_source=['doo'], hash_files=False, argstr='%s', position=1, name_template='%s_mootpl')
    poo = nib.File(name_source=['moo'], hash_files=False, argstr='%s', position=2)
    doo = nib.File(name_source=['poo'], hash_files=False, argstr='%s', position=3)

class TestCycle(nib.CommandLine):
    _cmd = 'mycommand'
    input_spec = spec3
to0 = TestCycle()
not_raised = True
try:
    to0.cmdline
except nib.NipypeInterfaceError:
    not_raised = False
assert not not_raised
```

## Next Steps


---

*Source: test_specs.py:256 | Complexity: Advanced | Last updated: 2026-05-18*