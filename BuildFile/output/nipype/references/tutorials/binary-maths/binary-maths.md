# How To: Binary Maths

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test binary maths

## Prerequisites

**Required Modules:**
- `pytest`
- `testing`
- `niftyreg`
- `niftyreg.tests.test_regutils`


## Step-by-Step Guide

### Step 1: Assign binarym = BinaryMaths(...)

```python
binarym = BinaryMaths()
```

**Verification:**
```python
assert binarym.cmd == cmd
```

### Step 2: Assign cmd = get_custom_path(...)

```python
cmd = get_custom_path('seg_maths', env_dir='NIFTYSEGDIR')
```

**Verification:**
```python
assert binarym.cmdline == expected_cmd
```

### Step 3: Assign in_file = example_data(...)

```python
in_file = example_data('im1.nii')
```

### Step 4: Assign binarym.inputs.in_file = in_file

```python
binarym.inputs.in_file = in_file
```

### Step 5: Assign binarym.inputs.operand_value = 2.0

```python
binarym.inputs.operand_value = 2.0
```

### Step 6: Assign binarym.inputs.operation = 'sub'

```python
binarym.inputs.operation = 'sub'
```

### Step 7: Assign binarym.inputs.output_datatype = 'float'

```python
binarym.inputs.output_datatype = 'float'
```

### Step 8: Assign cmd_tmp = '{cmd} {in_file} -sub 2.00000000 -odt float {out_file}'

```python
cmd_tmp = '{cmd} {in_file} -sub 2.00000000 -odt float {out_file}'
```

### Step 9: Assign expected_cmd = cmd_tmp.format(...)

```python
expected_cmd = cmd_tmp.format(cmd=cmd, in_file=in_file, out_file='im1_sub.nii')
```

**Verification:**
```python
assert binarym.cmdline == expected_cmd
```

### Step 10: Call binarym.run()

```python
binarym.run()
```


## Complete Example

```python
# Workflow
binarym = BinaryMaths()
cmd = get_custom_path('seg_maths', env_dir='NIFTYSEGDIR')
assert binarym.cmd == cmd
with pytest.raises(ValueError):
    binarym.run()
in_file = example_data('im1.nii')
binarym.inputs.in_file = in_file
binarym.inputs.operand_value = 2.0
binarym.inputs.operation = 'sub'
binarym.inputs.output_datatype = 'float'
cmd_tmp = '{cmd} {in_file} -sub 2.00000000 -odt float {out_file}'
expected_cmd = cmd_tmp.format(cmd=cmd, in_file=in_file, out_file='im1_sub.nii')
assert binarym.cmdline == expected_cmd
```

## Next Steps


---

*Source: test_maths.py:39 | Complexity: Advanced | Last updated: 2026-05-18*