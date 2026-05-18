# How To: Unary Maths

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test unary maths

## Prerequisites

**Required Modules:**
- `pytest`
- `testing`
- `niftyreg`
- `niftyreg.tests.test_regutils`


## Step-by-Step Guide

### Step 1: Assign unarym = UnaryMaths(...)

```python
unarym = UnaryMaths()
```

**Verification:**
```python
assert unarym.cmd == cmd
```

### Step 2: Assign cmd = get_custom_path(...)

```python
cmd = get_custom_path('seg_maths', env_dir='NIFTYSEGDIR')
```

**Verification:**
```python
assert unarym.cmdline == expected_cmd
```

### Step 3: Assign in_file = example_data(...)

```python
in_file = example_data('im1.nii')
```

### Step 4: Assign unarym.inputs.in_file = in_file

```python
unarym.inputs.in_file = in_file
```

### Step 5: Assign unarym.inputs.operation = 'otsu'

```python
unarym.inputs.operation = 'otsu'
```

### Step 6: Assign unarym.inputs.output_datatype = 'float'

```python
unarym.inputs.output_datatype = 'float'
```

### Step 7: Assign expected_cmd = unknown.format(...)

```python
expected_cmd = '{cmd} {in_file} -otsu -odt float {out_file}'.format(cmd=cmd, in_file=in_file, out_file='im1_otsu.nii')
```

**Verification:**
```python
assert unarym.cmdline == expected_cmd
```

### Step 8: Call unarym.run()

```python
unarym.run()
```


## Complete Example

```python
# Workflow
unarym = UnaryMaths()
cmd = get_custom_path('seg_maths', env_dir='NIFTYSEGDIR')
assert unarym.cmd == cmd
with pytest.raises(ValueError):
    unarym.run()
in_file = example_data('im1.nii')
unarym.inputs.in_file = in_file
unarym.inputs.operation = 'otsu'
unarym.inputs.output_datatype = 'float'
expected_cmd = '{cmd} {in_file} -otsu -odt float {out_file}'.format(cmd=cmd, in_file=in_file, out_file='im1_otsu.nii')
assert unarym.cmdline == expected_cmd
```

## Next Steps


---

*Source: test_maths.py:13 | Complexity: Advanced | Last updated: 2026-05-18*