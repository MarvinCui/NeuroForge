# How To: Gen Fname

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test gen fname

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `nipype.interfaces.fsl`
- `nipype.interfaces.base`
- `nipype.interfaces.fsl`
- `pytest`

**Setup Required:**
```python
# Fixtures: args, desired_name
```

## Step-by-Step Guide

### Step 1: Assign cmd = fsl.FSLCommand(...)

```python
cmd = fsl.FSLCommand(command='junk', output_type='NIFTI_GZ')
```

**Verification:**
```python
assert fname == desired
```

### Step 2: Assign pth = os.getcwd(...)

```python
pth = os.getcwd()
```

### Step 3: Assign fname = cmd._gen_fname(...)

```python
fname = cmd._gen_fname('foo.nii.gz', **args)
```

**Verification:**
```python
assert fname == desired
```

### Step 4: Assign desired = os.path.join(...)

```python
desired = os.path.join(desired_name['dir'], desired_name['file'])
```

### Step 5: Assign desired = os.path.join(...)

```python
desired = os.path.join(pth, desired_name['file'])
```


## Complete Example

```python
# Setup
# Fixtures: args, desired_name

# Workflow
cmd = fsl.FSLCommand(command='junk', output_type='NIFTI_GZ')
pth = os.getcwd()
fname = cmd._gen_fname('foo.nii.gz', **args)
if 'dir' in desired_name:
    desired = os.path.join(desired_name['dir'], desired_name['file'])
else:
    desired = os.path.join(pth, desired_name['file'])
assert fname == desired
```

## Next Steps


---

*Source: test_base.py:77 | Complexity: Intermediate | Last updated: 2026-05-18*