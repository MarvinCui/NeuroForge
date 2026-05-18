# How To: Reg Tools Mul

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: tests for reg_tools interface

## Prerequisites

**Required Modules:**
- `os`
- `pytest`
- `utils.filemanip`
- `testing`


## Step-by-Step Guide

### Step 1: 'tests for reg_tools interface'

```python
'tests for reg_tools interface'
```

**Verification:**
```python
assert nr_tools.cmd == get_custom_path('reg_tools')
```

### Step 2: Assign nr_tools = RegTools(...)

```python
nr_tools = RegTools()
```

**Verification:**
```python
assert nr_tools.cmdline == expected_cmd
```

### Step 3: Assign in_file = example_data(...)

```python
in_file = example_data('im1.nii')
```

**Verification:**
```python
assert nr_tools_2.cmdline == expected_cmd
```

### Step 4: Assign nr_tools.inputs.in_file = in_file

```python
nr_tools.inputs.in_file = in_file
```

### Step 5: Assign nr_tools.inputs.mul_val = 4

```python
nr_tools.inputs.mul_val = 4
```

### Step 6: Assign nr_tools.inputs.omp_core_val = 4

```python
nr_tools.inputs.omp_core_val = 4
```

### Step 7: Assign cmd_tmp = '{cmd} -in {in_file} -mul 4.0 -omp 4 -out {out_file}'

```python
cmd_tmp = '{cmd} -in {in_file} -mul 4.0 -omp 4 -out {out_file}'
```

### Step 8: Assign expected_cmd = cmd_tmp.format(...)

```python
expected_cmd = cmd_tmp.format(cmd=get_custom_path('reg_tools'), in_file=in_file, out_file='im1_tools.nii.gz')
```

**Verification:**
```python
assert nr_tools.cmdline == expected_cmd
```

### Step 9: Assign nr_tools_2 = RegTools(...)

```python
nr_tools_2 = RegTools(iso_flag=True, omp_core_val=4)
```

### Step 10: Assign in_file = example_data(...)

```python
in_file = example_data('im1.nii')
```

### Step 11: Assign nr_tools_2.inputs.in_file = in_file

```python
nr_tools_2.inputs.in_file = in_file
```

### Step 12: Assign cmd_tmp = '{cmd} -in {in_file} -iso -omp 4 -out {out_file}'

```python
cmd_tmp = '{cmd} -in {in_file} -iso -omp 4 -out {out_file}'
```

### Step 13: Assign expected_cmd = cmd_tmp.format(...)

```python
expected_cmd = cmd_tmp.format(cmd=get_custom_path('reg_tools'), in_file=in_file, out_file='im1_tools.nii.gz')
```

**Verification:**
```python
assert nr_tools_2.cmdline == expected_cmd
```

### Step 14: Call nr_tools.run()

```python
nr_tools.run()
```


## Complete Example

```python
# Workflow
'tests for reg_tools interface'
nr_tools = RegTools()
assert nr_tools.cmd == get_custom_path('reg_tools')
with pytest.raises(ValueError):
    nr_tools.run()
in_file = example_data('im1.nii')
nr_tools.inputs.in_file = in_file
nr_tools.inputs.mul_val = 4
nr_tools.inputs.omp_core_val = 4
cmd_tmp = '{cmd} -in {in_file} -mul 4.0 -omp 4 -out {out_file}'
expected_cmd = cmd_tmp.format(cmd=get_custom_path('reg_tools'), in_file=in_file, out_file='im1_tools.nii.gz')
assert nr_tools.cmdline == expected_cmd
nr_tools_2 = RegTools(iso_flag=True, omp_core_val=4)
in_file = example_data('im1.nii')
nr_tools_2.inputs.in_file = in_file
cmd_tmp = '{cmd} -in {in_file} -iso -omp 4 -out {out_file}'
expected_cmd = cmd_tmp.format(cmd=get_custom_path('reg_tools'), in_file=in_file, out_file='im1_tools.nii.gz')
assert nr_tools_2.cmdline == expected_cmd
```

## Next Steps


---

*Source: test_regutils.py:157 | Complexity: Advanced | Last updated: 2026-05-18*