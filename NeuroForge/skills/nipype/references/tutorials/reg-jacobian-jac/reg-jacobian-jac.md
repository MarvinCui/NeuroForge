# How To: Reg Jacobian Jac

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test interface for RegJacobian

## Prerequisites

**Required Modules:**
- `os`
- `pytest`
- `utils.filemanip`
- `testing`


## Step-by-Step Guide

### Step 1: 'Test interface for RegJacobian'

```python
'Test interface for RegJacobian'
```

**Verification:**
```python
assert nr_jacobian.cmd == get_custom_path('reg_jacobian')
```

### Step 2: Assign nr_jacobian = RegJacobian(...)

```python
nr_jacobian = RegJacobian()
```

**Verification:**
```python
assert nr_jacobian.cmdline == expected_cmd
```

### Step 3: Assign ref_file = example_data(...)

```python
ref_file = example_data('im1.nii')
```

**Verification:**
```python
assert nr_jacobian_2.cmdline == expected_cmd
```

### Step 4: Assign trans_file = example_data(...)

```python
trans_file = example_data('warpfield.nii')
```

**Verification:**
```python
assert nr_jacobian_3.cmdline == expected_cmd
```

### Step 5: Assign nr_jacobian.inputs.ref_file = ref_file

```python
nr_jacobian.inputs.ref_file = ref_file
```

### Step 6: Assign nr_jacobian.inputs.trans_file = trans_file

```python
nr_jacobian.inputs.trans_file = trans_file
```

### Step 7: Assign nr_jacobian.inputs.omp_core_val = 4

```python
nr_jacobian.inputs.omp_core_val = 4
```

### Step 8: Assign cmd_tmp = '{cmd} -omp 4 -ref {ref} -trans {trans} -jac {jac}'

```python
cmd_tmp = '{cmd} -omp 4 -ref {ref} -trans {trans} -jac {jac}'
```

### Step 9: Assign expected_cmd = cmd_tmp.format(...)

```python
expected_cmd = cmd_tmp.format(cmd=get_custom_path('reg_jacobian'), ref=ref_file, trans=trans_file, jac='warpfield_jac.nii.gz')
```

**Verification:**
```python
assert nr_jacobian.cmdline == expected_cmd
```

### Step 10: Assign nr_jacobian_2 = RegJacobian(...)

```python
nr_jacobian_2 = RegJacobian(type='jacM', omp_core_val=4)
```

### Step 11: Assign ref_file = example_data(...)

```python
ref_file = example_data('im1.nii')
```

### Step 12: Assign trans_file = example_data(...)

```python
trans_file = example_data('warpfield.nii')
```

### Step 13: Assign nr_jacobian_2.inputs.ref_file = ref_file

```python
nr_jacobian_2.inputs.ref_file = ref_file
```

### Step 14: Assign nr_jacobian_2.inputs.trans_file = trans_file

```python
nr_jacobian_2.inputs.trans_file = trans_file
```

### Step 15: Assign cmd_tmp = '{cmd} -omp 4 -ref {ref} -trans {trans} -jacM {jac}'

```python
cmd_tmp = '{cmd} -omp 4 -ref {ref} -trans {trans} -jacM {jac}'
```

### Step 16: Assign expected_cmd = cmd_tmp.format(...)

```python
expected_cmd = cmd_tmp.format(cmd=get_custom_path('reg_jacobian'), ref=ref_file, trans=trans_file, jac='warpfield_jacM.nii.gz')
```

**Verification:**
```python
assert nr_jacobian_2.cmdline == expected_cmd
```

### Step 17: Assign nr_jacobian_3 = RegJacobian(...)

```python
nr_jacobian_3 = RegJacobian(type='jacL', omp_core_val=4)
```

### Step 18: Assign ref_file = example_data(...)

```python
ref_file = example_data('im1.nii')
```

### Step 19: Assign trans_file = example_data(...)

```python
trans_file = example_data('warpfield.nii')
```

### Step 20: Assign nr_jacobian_3.inputs.ref_file = ref_file

```python
nr_jacobian_3.inputs.ref_file = ref_file
```

### Step 21: Assign nr_jacobian_3.inputs.trans_file = trans_file

```python
nr_jacobian_3.inputs.trans_file = trans_file
```

### Step 22: Assign cmd_tmp = '{cmd} -omp 4 -ref {ref} -trans {trans} -jacL {jac}'

```python
cmd_tmp = '{cmd} -omp 4 -ref {ref} -trans {trans} -jacL {jac}'
```

### Step 23: Assign expected_cmd = cmd_tmp.format(...)

```python
expected_cmd = cmd_tmp.format(cmd=get_custom_path('reg_jacobian'), ref=ref_file, trans=trans_file, jac='warpfield_jacL.nii.gz')
```

**Verification:**
```python
assert nr_jacobian_3.cmdline == expected_cmd
```

### Step 24: Call nr_jacobian.run()

```python
nr_jacobian.run()
```


## Complete Example

```python
# Workflow
'Test interface for RegJacobian'
nr_jacobian = RegJacobian()
assert nr_jacobian.cmd == get_custom_path('reg_jacobian')
with pytest.raises(ValueError):
    nr_jacobian.run()
ref_file = example_data('im1.nii')
trans_file = example_data('warpfield.nii')
nr_jacobian.inputs.ref_file = ref_file
nr_jacobian.inputs.trans_file = trans_file
nr_jacobian.inputs.omp_core_val = 4
cmd_tmp = '{cmd} -omp 4 -ref {ref} -trans {trans} -jac {jac}'
expected_cmd = cmd_tmp.format(cmd=get_custom_path('reg_jacobian'), ref=ref_file, trans=trans_file, jac='warpfield_jac.nii.gz')
assert nr_jacobian.cmdline == expected_cmd
nr_jacobian_2 = RegJacobian(type='jacM', omp_core_val=4)
ref_file = example_data('im1.nii')
trans_file = example_data('warpfield.nii')
nr_jacobian_2.inputs.ref_file = ref_file
nr_jacobian_2.inputs.trans_file = trans_file
cmd_tmp = '{cmd} -omp 4 -ref {ref} -trans {trans} -jacM {jac}'
expected_cmd = cmd_tmp.format(cmd=get_custom_path('reg_jacobian'), ref=ref_file, trans=trans_file, jac='warpfield_jacM.nii.gz')
assert nr_jacobian_2.cmdline == expected_cmd
nr_jacobian_3 = RegJacobian(type='jacL', omp_core_val=4)
ref_file = example_data('im1.nii')
trans_file = example_data('warpfield.nii')
nr_jacobian_3.inputs.ref_file = ref_file
nr_jacobian_3.inputs.trans_file = trans_file
cmd_tmp = '{cmd} -omp 4 -ref {ref} -trans {trans} -jacL {jac}'
expected_cmd = cmd_tmp.format(cmd=get_custom_path('reg_jacobian'), ref=ref_file, trans=trans_file, jac='warpfield_jacL.nii.gz')
assert nr_jacobian_3.cmdline == expected_cmd
```

## Next Steps


---

*Source: test_regutils.py:89 | Complexity: Advanced | Last updated: 2026-05-18*