# How To: Tuple Maths

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test tuple maths

## Prerequisites

**Required Modules:**
- `pytest`
- `testing`
- `niftyreg`
- `niftyreg.tests.test_regutils`


## Step-by-Step Guide

### Step 1: Assign tuplem = TupleMaths(...)

```python
tuplem = TupleMaths()
```

**Verification:**
```python
assert tuplem.cmd == cmd
```

### Step 2: Assign cmd = get_custom_path(...)

```python
cmd = get_custom_path('seg_maths', env_dir='NIFTYSEGDIR')
```

**Verification:**
```python
assert tuplem.cmdline == expected_cmd
```

### Step 3: Assign in_file = example_data(...)

```python
in_file = example_data('im1.nii')
```

### Step 4: Assign op_file = example_data(...)

```python
op_file = example_data('im2.nii')
```

### Step 5: Assign tuplem.inputs.in_file = in_file

```python
tuplem.inputs.in_file = in_file
```

### Step 6: Assign tuplem.inputs.operation = 'lncc'

```python
tuplem.inputs.operation = 'lncc'
```

### Step 7: Assign tuplem.inputs.operand_file1 = op_file

```python
tuplem.inputs.operand_file1 = op_file
```

### Step 8: Assign tuplem.inputs.operand_value2 = 2.0

```python
tuplem.inputs.operand_value2 = 2.0
```

### Step 9: Assign tuplem.inputs.output_datatype = 'float'

```python
tuplem.inputs.output_datatype = 'float'
```

### Step 10: Assign cmd_tmp = '{cmd} {in_file} -lncc {op} 2.00000000 -odt float {out_file}'

```python
cmd_tmp = '{cmd} {in_file} -lncc {op} 2.00000000 -odt float {out_file}'
```

### Step 11: Assign expected_cmd = cmd_tmp.format(...)

```python
expected_cmd = cmd_tmp.format(cmd=cmd, in_file=in_file, op=op_file, out_file='im1_lncc.nii')
```

**Verification:**
```python
assert tuplem.cmdline == expected_cmd
```

### Step 12: Call tuplem.run()

```python
tuplem.run()
```


## Complete Example

```python
# Workflow
tuplem = TupleMaths()
cmd = get_custom_path('seg_maths', env_dir='NIFTYSEGDIR')
assert tuplem.cmd == cmd
with pytest.raises(ValueError):
    tuplem.run()
in_file = example_data('im1.nii')
op_file = example_data('im2.nii')
tuplem.inputs.in_file = in_file
tuplem.inputs.operation = 'lncc'
tuplem.inputs.operand_file1 = op_file
tuplem.inputs.operand_value2 = 2.0
tuplem.inputs.output_datatype = 'float'
cmd_tmp = '{cmd} {in_file} -lncc {op} 2.00000000 -odt float {out_file}'
expected_cmd = cmd_tmp.format(cmd=cmd, in_file=in_file, op=op_file, out_file='im1_lncc.nii')
assert tuplem.cmdline == expected_cmd
```

## Next Steps


---

*Source: test_maths.py:92 | Complexity: Advanced | Last updated: 2026-05-18*