# How To: Cycle Namesource2

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test cycle namesource2

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
assert not_raised
```

### Step 2: Assign unknown = split_filename(...)

```python
tmpd, nme, ext = split_filename(tmp_infile)
```

**Verification:**
```python
assert '%s' % tmp_infile in res
```

### Step 3: Assign to1 = TestCycle(...)

```python
to1 = TestCycle()
```

**Verification:**
```python
assert '%s_generated' % nme in res
```

### Step 4: Assign to1.inputs.poo = tmp_infile

```python
to1.inputs.poo = tmp_infile
```

**Verification:**
```python
assert '%s_generated_mootpl' % nme in res
```

### Step 5: Assign not_raised = True

```python
not_raised = True
```

### Step 6: Call print()

```python
print(res)
```

**Verification:**
```python
assert not_raised
```

### Step 7: Assign moo = nib.File(...)

```python
moo = nib.File(name_source=['doo'], hash_files=False, argstr='%s', position=1, name_template='%s_mootpl')
```

### Step 8: Assign poo = nib.File(...)

```python
poo = nib.File(name_source=['moo'], hash_files=False, argstr='%s', position=2)
```

### Step 9: Assign doo = nib.File(...)

```python
doo = nib.File(name_source=['poo'], hash_files=False, argstr='%s', position=3)
```

### Step 10: Assign _cmd = 'mycommand'

```python
_cmd = 'mycommand'
```

### Step 11: Assign input_spec = spec3

```python
input_spec = spec3
```

### Step 12: Assign res = value

```python
res = to1.cmdline
```

### Step 13: Assign not_raised = False

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
to1 = TestCycle()
to1.inputs.poo = tmp_infile
not_raised = True
try:
    res = to1.cmdline
except nib.NipypeInterfaceError:
    not_raised = False
print(res)
assert not_raised
assert '%s' % tmp_infile in res
assert '%s_generated' % nme in res
assert '%s_generated_mootpl' % nme in res
```

## Next Steps


---

*Source: test_specs.py:285 | Complexity: Advanced | Last updated: 2026-05-18*