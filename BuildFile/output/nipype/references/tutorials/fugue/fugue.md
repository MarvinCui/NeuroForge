# How To: Fugue

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test fugue

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `copy`
- `pytest`
- `nipype.utils.filemanip`
- `nipype.interfaces.fsl`
- `nipype.interfaces.base`
- `nipype.interfaces.fsl`
- `nibabel`
- `numpy`
- `os.path`

**Setup Required:**
```python
# Fixtures: setup_fugue, attr, out_file
```

## Step-by-Step Guide

### Step 1: Assign unknown = setup_fugue

```python
tmpdir, infile = setup_fugue
```

**Verification:**
```python
assert isdefined(getattr(res.outputs, out_file))
```

### Step 2: Assign fugue = fsl.FUGUE(...)

```python
fugue = fsl.FUGUE()
```

**Verification:**
```python
assert op.basename(getattr(res.outputs, out_file)) == out_name
```

### Step 3: Assign res = fugue.run(...)

```python
res = fugue.run()
```

**Verification:**
```python
assert isdefined(getattr(res.outputs, out_file))
```

### Step 4: Assign trait_spec = fugue.inputs.trait(...)

```python
trait_spec = fugue.inputs.trait(out_file)
```

### Step 5: Assign out_name = value

```python
out_name = trait_spec.name_template % 'dumbfile'
```

**Verification:**
```python
assert op.basename(getattr(res.outputs, out_file)) == out_name
```

### Step 6: Call setattr()

```python
setattr(fugue.inputs, key, infile)
```

### Step 7: Call setattr()

```python
setattr(fugue.inputs, key, value)
```


## Complete Example

```python
# Setup
# Fixtures: setup_fugue, attr, out_file

# Workflow
import os.path as op
tmpdir, infile = setup_fugue
fugue = fsl.FUGUE()
for key, value in attr.items():
    if value == 'infile':
        setattr(fugue.inputs, key, infile)
    else:
        setattr(fugue.inputs, key, value)
res = fugue.run()
assert isdefined(getattr(res.outputs, out_file))
trait_spec = fugue.inputs.trait(out_file)
out_name = trait_spec.name_template % 'dumbfile'
out_name += '.nii.gz'
assert op.basename(getattr(res.outputs, out_file)) == out_name
```

## Next Steps


---

*Source: test_preprocess.py:623 | Complexity: Intermediate | Last updated: 2026-05-18*