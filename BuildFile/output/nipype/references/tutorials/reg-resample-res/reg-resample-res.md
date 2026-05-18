# How To: Reg Resample Res

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: tests for reg_resample interface

## Prerequisites

**Required Modules:**
- `os`
- `pytest`
- `utils.filemanip`
- `testing`


## Step-by-Step Guide

### Step 1: 'tests for reg_resample interface'

```python
'tests for reg_resample interface'
```

**Verification:**
```python
assert nr_resample.cmd == get_custom_path('reg_resample')
```

### Step 2: Assign nr_resample = RegResample(...)

```python
nr_resample = RegResample()
```

**Verification:**
```python
assert nr_resample.cmdline == expected_cmd
```

### Step 3: Assign ref_file = example_data(...)

```python
ref_file = example_data('im1.nii')
```

**Verification:**
```python
assert nr_resample_2.cmdline == expected_cmd
```

### Step 4: Assign flo_file = example_data(...)

```python
flo_file = example_data('im2.nii')
```

### Step 5: Assign trans_file = example_data(...)

```python
trans_file = example_data('warpfield.nii')
```

### Step 6: Assign nr_resample.inputs.ref_file = ref_file

```python
nr_resample.inputs.ref_file = ref_file
```

### Step 7: Assign nr_resample.inputs.flo_file = flo_file

```python
nr_resample.inputs.flo_file = flo_file
```

### Step 8: Assign nr_resample.inputs.trans_file = trans_file

```python
nr_resample.inputs.trans_file = trans_file
```

### Step 9: Assign nr_resample.inputs.inter_val = 'LIN'

```python
nr_resample.inputs.inter_val = 'LIN'
```

### Step 10: Assign nr_resample.inputs.omp_core_val = 4

```python
nr_resample.inputs.omp_core_val = 4
```

### Step 11: Assign cmd_tmp = '{cmd} -flo {flo} -inter 1 -omp 4 -ref {ref} -trans {trans} -res {res}'

```python
cmd_tmp = '{cmd} -flo {flo} -inter 1 -omp 4 -ref {ref} -trans {trans} -res {res}'
```

### Step 12: Assign expected_cmd = cmd_tmp.format(...)

```python
expected_cmd = cmd_tmp.format(cmd=get_custom_path('reg_resample'), flo=flo_file, ref=ref_file, trans=trans_file, res='im2_res.nii.gz')
```

**Verification:**
```python
assert nr_resample.cmdline == expected_cmd
```

### Step 13: Assign nr_resample_2 = RegResample(...)

```python
nr_resample_2 = RegResample(type='blank', inter_val='LIN', omp_core_val=4)
```

### Step 14: Assign ref_file = example_data(...)

```python
ref_file = example_data('im1.nii')
```

### Step 15: Assign flo_file = example_data(...)

```python
flo_file = example_data('im2.nii')
```

### Step 16: Assign trans_file = example_data(...)

```python
trans_file = example_data('warpfield.nii')
```

### Step 17: Assign nr_resample_2.inputs.ref_file = ref_file

```python
nr_resample_2.inputs.ref_file = ref_file
```

### Step 18: Assign nr_resample_2.inputs.flo_file = flo_file

```python
nr_resample_2.inputs.flo_file = flo_file
```

### Step 19: Assign nr_resample_2.inputs.trans_file = trans_file

```python
nr_resample_2.inputs.trans_file = trans_file
```

### Step 20: Assign cmd_tmp = '{cmd} -flo {flo} -inter 1 -omp 4 -ref {ref} -trans {trans} -blank {blank}'

```python
cmd_tmp = '{cmd} -flo {flo} -inter 1 -omp 4 -ref {ref} -trans {trans} -blank {blank}'
```

### Step 21: Assign expected_cmd = cmd_tmp.format(...)

```python
expected_cmd = cmd_tmp.format(cmd=get_custom_path('reg_resample'), flo=flo_file, ref=ref_file, trans=trans_file, blank='im2_blank.nii.gz')
```

**Verification:**
```python
assert nr_resample_2.cmdline == expected_cmd
```

### Step 22: Call nr_resample.run()

```python
nr_resample.run()
```


## Complete Example

```python
# Workflow
'tests for reg_resample interface'
nr_resample = RegResample()
assert nr_resample.cmd == get_custom_path('reg_resample')
with pytest.raises(ValueError):
    nr_resample.run()
ref_file = example_data('im1.nii')
flo_file = example_data('im2.nii')
trans_file = example_data('warpfield.nii')
nr_resample.inputs.ref_file = ref_file
nr_resample.inputs.flo_file = flo_file
nr_resample.inputs.trans_file = trans_file
nr_resample.inputs.inter_val = 'LIN'
nr_resample.inputs.omp_core_val = 4
cmd_tmp = '{cmd} -flo {flo} -inter 1 -omp 4 -ref {ref} -trans {trans} -res {res}'
expected_cmd = cmd_tmp.format(cmd=get_custom_path('reg_resample'), flo=flo_file, ref=ref_file, trans=trans_file, res='im2_res.nii.gz')
assert nr_resample.cmdline == expected_cmd
nr_resample_2 = RegResample(type='blank', inter_val='LIN', omp_core_val=4)
ref_file = example_data('im1.nii')
flo_file = example_data('im2.nii')
trans_file = example_data('warpfield.nii')
nr_resample_2.inputs.ref_file = ref_file
nr_resample_2.inputs.flo_file = flo_file
nr_resample_2.inputs.trans_file = trans_file
cmd_tmp = '{cmd} -flo {flo} -inter 1 -omp 4 -ref {ref} -trans {trans} -blank {blank}'
expected_cmd = cmd_tmp.format(cmd=get_custom_path('reg_resample'), flo=flo_file, ref=ref_file, trans=trans_file, blank='im2_blank.nii.gz')
assert nr_resample_2.cmdline == expected_cmd
```

## Next Steps


---

*Source: test_regutils.py:27 | Complexity: Advanced | Last updated: 2026-05-18*