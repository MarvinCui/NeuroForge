# How To: Seg Calctopncc

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test interfaces for seg_CalctoNCC

## Prerequisites

**Required Modules:**
- `pytest`
- `testing`
- `niftyreg`
- `niftyreg.tests.test_regutils`


## Step-by-Step Guide

### Step 1: 'Test interfaces for seg_CalctoNCC'

```python
'Test interfaces for seg_CalctoNCC'
```

**Verification:**
```python
assert calctopncc.cmd == cmd
```

### Step 2: Assign calctopncc = CalcTopNCC(...)

```python
calctopncc = CalcTopNCC()
```

**Verification:**
```python
assert calctopncc.cmdline == expected_cmd
```

### Step 3: Assign cmd = get_custom_path(...)

```python
cmd = get_custom_path('seg_CalcTopNCC', env_dir='NIFTYSEGDIR')
```

**Verification:**
```python
assert calctopncc.cmd == cmd
```

### Step 4: Assign in_file = example_data(...)

```python
in_file = example_data('im1.nii')
```

### Step 5: Assign file1 = example_data(...)

```python
file1 = example_data('im2.nii')
```

### Step 6: Assign file2 = example_data(...)

```python
file2 = example_data('im3.nii')
```

### Step 7: Assign calctopncc.inputs.in_file = in_file

```python
calctopncc.inputs.in_file = in_file
```

### Step 8: Assign calctopncc.inputs.num_templates = 2

```python
calctopncc.inputs.num_templates = 2
```

### Step 9: Assign calctopncc.inputs.in_templates = value

```python
calctopncc.inputs.in_templates = [file1, file2]
```

### Step 10: Assign calctopncc.inputs.top_templates = 1

```python
calctopncc.inputs.top_templates = 1
```

### Step 11: Assign cmd_tmp = '{cmd} -target {in_file} -templates 2 {file1} {file2} -n 1'

```python
cmd_tmp = '{cmd} -target {in_file} -templates 2 {file1} {file2} -n 1'
```

### Step 12: Assign expected_cmd = cmd_tmp.format(...)

```python
expected_cmd = cmd_tmp.format(cmd=cmd, in_file=in_file, file1=file1, file2=file2)
```

**Verification:**
```python
assert calctopncc.cmdline == expected_cmd
```

### Step 13: Call calctopncc.run()

```python
calctopncc.run()
```


## Complete Example

```python
# Workflow
'Test interfaces for seg_CalctoNCC'
calctopncc = CalcTopNCC()
cmd = get_custom_path('seg_CalcTopNCC', env_dir='NIFTYSEGDIR')
assert calctopncc.cmd == cmd
with pytest.raises(ValueError):
    calctopncc.run()
in_file = example_data('im1.nii')
file1 = example_data('im2.nii')
file2 = example_data('im3.nii')
calctopncc.inputs.in_file = in_file
calctopncc.inputs.num_templates = 2
calctopncc.inputs.in_templates = [file1, file2]
calctopncc.inputs.top_templates = 1
cmd_tmp = '{cmd} -target {in_file} -templates 2 {file1} {file2} -n 1'
expected_cmd = cmd_tmp.format(cmd=cmd, in_file=in_file, file1=file1, file2=file2)
assert calctopncc.cmdline == expected_cmd
```

## Next Steps


---

*Source: test_label_fusion.py:100 | Complexity: Advanced | Last updated: 2026-05-18*