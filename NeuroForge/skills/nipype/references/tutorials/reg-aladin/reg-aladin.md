# How To: Reg Aladin

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: tests for reg_aladin interface

## Prerequisites

**Required Modules:**
- `pytest`
- `testing`
- `test_regutils`


## Step-by-Step Guide

### Step 1: 'tests for reg_aladin interface'

```python
'tests for reg_aladin interface'
```

**Verification:**
```python
assert nr_aladin.cmd == get_custom_path('reg_aladin')
```

### Step 2: Assign nr_aladin = RegAladin(...)

```python
nr_aladin = RegAladin()
```

**Verification:**
```python
assert nr_aladin.cmdline == expected_cmd
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

### Step 6: Assign nr_aladin.inputs.ref_file = ref_file

```python
nr_aladin.inputs.ref_file = ref_file
```

### Step 7: Assign nr_aladin.inputs.flo_file = flo_file

```python
nr_aladin.inputs.flo_file = flo_file
```

### Step 8: Assign nr_aladin.inputs.rmask_file = rmask_file

```python
nr_aladin.inputs.rmask_file = rmask_file
```

### Step 9: Assign nr_aladin.inputs.omp_core_val = 4

```python
nr_aladin.inputs.omp_core_val = 4
```

### Step 10: Assign cmd_tmp = '{cmd} -aff {aff} -flo {flo} -omp 4 -ref {ref} -res {res} -rmask {rmask}'

```python
cmd_tmp = '{cmd} -aff {aff} -flo {flo} -omp 4 -ref {ref} -res {res} -rmask {rmask}'
```

### Step 11: Assign expected_cmd = cmd_tmp.format(...)

```python
expected_cmd = cmd_tmp.format(cmd=get_custom_path('reg_aladin'), aff='im2_aff.txt', flo=flo_file, ref=ref_file, res='im2_res.nii.gz', rmask=rmask_file)
```

**Verification:**
```python
assert nr_aladin.cmdline == expected_cmd
```

### Step 12: Call nr_aladin.run()

```python
nr_aladin.run()
```


## Complete Example

```python
# Workflow
'tests for reg_aladin interface'
nr_aladin = RegAladin()
assert nr_aladin.cmd == get_custom_path('reg_aladin')
with pytest.raises(ValueError):
    nr_aladin.run()
ref_file = example_data('im1.nii')
flo_file = example_data('im2.nii')
rmask_file = example_data('mask.nii')
nr_aladin.inputs.ref_file = ref_file
nr_aladin.inputs.flo_file = flo_file
nr_aladin.inputs.rmask_file = rmask_file
nr_aladin.inputs.omp_core_val = 4
cmd_tmp = '{cmd} -aff {aff} -flo {flo} -omp 4 -ref {ref} -res {res} -rmask {rmask}'
expected_cmd = cmd_tmp.format(cmd=get_custom_path('reg_aladin'), aff='im2_aff.txt', flo=flo_file, ref=ref_file, res='im2_res.nii.gz', rmask=rmask_file)
assert nr_aladin.cmdline == expected_cmd
```

## Next Steps


---

*Source: test_reg.py:15 | Complexity: Advanced | Last updated: 2026-05-18*