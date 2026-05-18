# How To: Int Binary Maths

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test int binary maths

## Prerequisites

**Required Modules:**
- `pytest`
- `testing`
- `niftyreg`
- `niftyreg.tests.test_regutils`


## Step-by-Step Guide

### Step 1: Assign ibinarym = BinaryMathsInteger(...)

```python
ibinarym = BinaryMathsInteger()
```

**Verification:**
```python
assert ibinarym.cmd == cmd
```

### Step 2: Assign cmd = get_custom_path(...)

```python
cmd = get_custom_path('seg_maths', env_dir='NIFTYSEGDIR')
```

**Verification:**
```python
assert ibinarym.cmdline == expected_cmd
```

### Step 3: Assign in_file = example_data(...)

```python
in_file = example_data('im1.nii')
```

### Step 4: Assign ibinarym.inputs.in_file = in_file

```python
ibinarym.inputs.in_file = in_file
```

### Step 5: Assign ibinarym.inputs.operand_value = 2

```python
ibinarym.inputs.operand_value = 2
```

### Step 6: Assign ibinarym.inputs.operation = 'dil'

```python
ibinarym.inputs.operation = 'dil'
```

### Step 7: Assign ibinarym.inputs.output_datatype = 'float'

```python
ibinarym.inputs.output_datatype = 'float'
```

### Step 8: Assign expected_cmd = unknown.format(...)

```python
expected_cmd = '{cmd} {in_file} -dil 2 -odt float {out_file}'.format(cmd=cmd, in_file=in_file, out_file='im1_dil.nii')
```

**Verification:**
```python
assert ibinarym.cmdline == expected_cmd
```

### Step 9: Call ibinarym.run()

```python
ibinarym.run()
```


## Complete Example

```python
# Workflow
ibinarym = BinaryMathsInteger()
cmd = get_custom_path('seg_maths', env_dir='NIFTYSEGDIR')
assert ibinarym.cmd == cmd
with pytest.raises(ValueError):
    ibinarym.run()
in_file = example_data('im1.nii')
ibinarym.inputs.in_file = in_file
ibinarym.inputs.operand_value = 2
ibinarym.inputs.operation = 'dil'
ibinarym.inputs.output_datatype = 'float'
expected_cmd = '{cmd} {in_file} -dil 2 -odt float {out_file}'.format(cmd=cmd, in_file=in_file, out_file='im1_dil.nii')
assert ibinarym.cmdline == expected_cmd
```

## Next Steps


---

*Source: test_maths.py:65 | Complexity: Advanced | Last updated: 2026-05-18*