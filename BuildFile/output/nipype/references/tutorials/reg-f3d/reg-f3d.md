# How To: Reg F3D

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: tests for reg_f3d interface

## Prerequisites

**Required Modules:**
- `pytest`
- `testing`
- `test_regutils`


## Step-by-Step Guide

### Step 1: 'tests for reg_f3d interface'

```python
'tests for reg_f3d interface'
```

**Verification:**
```python
assert nr_f3d.cmd == get_custom_path('reg_f3d')
```

### Step 2: Assign nr_f3d = RegF3D(...)

```python
nr_f3d = RegF3D()
```

**Verification:**
```python
assert nr_f3d.cmdline == expected_cmd
```

### Step 3: Assign ref_file = example_data(...)

```python
ref_file = example_data('im1.nii')
```

### Step 4: Assign flo_file = example_data(...)

```python
flo_file = example_data('im2.nii')
```

### Step 5: Assign rmask_file = example_data(...)

```python
rmask_file = example_data('mask.nii')
```

### Step 6: Assign nr_f3d.inputs.ref_file = ref_file

```python
nr_f3d.inputs.ref_file = ref_file
```

### Step 7: Assign nr_f3d.inputs.flo_file = flo_file

```python
nr_f3d.inputs.flo_file = flo_file
```

### Step 8: Assign nr_f3d.inputs.rmask_file = rmask_file

```python
nr_f3d.inputs.rmask_file = rmask_file
```

### Step 9: Assign nr_f3d.inputs.omp_core_val = 4

```python
nr_f3d.inputs.omp_core_val = 4
```

### Step 10: Assign nr_f3d.inputs.vel_flag = True

```python
nr_f3d.inputs.vel_flag = True
```

### Step 11: Assign nr_f3d.inputs.be_val = 0.1

```python
nr_f3d.inputs.be_val = 0.1
```

### Step 12: Assign nr_f3d.inputs.le_val = 0.1

```python
nr_f3d.inputs.le_val = 0.1
```

### Step 13: Assign cmd_tmp = '{cmd} -be 0.100000 -cpp {cpp} -flo {flo} -le 0.100000 -omp 4 -ref {ref} -res {res} -rmask {rmask} -vel'

```python
cmd_tmp = '{cmd} -be 0.100000 -cpp {cpp} -flo {flo} -le 0.100000 -omp 4 -ref {ref} -res {res} -rmask {rmask} -vel'
```

### Step 14: Assign expected_cmd = cmd_tmp.format(...)

```python
expected_cmd = cmd_tmp.format(cmd=get_custom_path('reg_f3d'), cpp='im2_cpp.nii.gz', flo=flo_file, ref=ref_file, res='im2_res.nii.gz', rmask=rmask_file)
```

**Verification:**
```python
assert nr_f3d.cmdline == expected_cmd
```

### Step 15: Call nr_f3d.run()

```python
nr_f3d.run()
```


## Complete Example

```python
# Workflow
'tests for reg_f3d interface'
nr_f3d = RegF3D()
assert nr_f3d.cmd == get_custom_path('reg_f3d')
with pytest.raises(ValueError):
    nr_f3d.run()
ref_file = example_data('im1.nii')
flo_file = example_data('im2.nii')
rmask_file = example_data('mask.nii')
nr_f3d.inputs.ref_file = ref_file
nr_f3d.inputs.flo_file = flo_file
nr_f3d.inputs.rmask_file = rmask_file
nr_f3d.inputs.omp_core_val = 4
nr_f3d.inputs.vel_flag = True
nr_f3d.inputs.be_val = 0.1
nr_f3d.inputs.le_val = 0.1
cmd_tmp = '{cmd} -be 0.100000 -cpp {cpp} -flo {flo} -le 0.100000 -omp 4 -ref {ref} -res {res} -rmask {rmask} -vel'
expected_cmd = cmd_tmp.format(cmd=get_custom_path('reg_f3d'), cpp='im2_cpp.nii.gz', flo=flo_file, ref=ref_file, res='im2_res.nii.gz', rmask=rmask_file)
assert nr_f3d.cmdline == expected_cmd
```

## Next Steps


---

*Source: test_reg.py:54 | Complexity: Advanced | Last updated: 2026-05-18*