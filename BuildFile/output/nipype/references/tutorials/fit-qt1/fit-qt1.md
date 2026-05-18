# How To: Fit Qt1

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Testing FitQt1 interface.

## Prerequisites

**Required Modules:**
- `pytest`
- `testing`
- `niftyreg`
- `niftyreg.tests.test_regutils`
- `qt1`


## Step-by-Step Guide

### Step 1: 'Testing FitQt1 interface.'

```python
'Testing FitQt1 interface.'
```

**Verification:**
```python
assert fit_qt1.cmd == cmd
```

### Step 2: Assign fit_qt1 = FitQt1(...)

```python
fit_qt1 = FitQt1()
```

**Verification:**
```python
assert fit_qt1.cmdline == expected_cmd
```

### Step 3: Assign cmd = get_custom_path(...)

```python
cmd = get_custom_path('fit_qt1', env_dir='NIFTYFITDIR')
```

**Verification:**
```python
assert fit_qt1_2.cmdline == expected_cmd
```

### Step 4: Assign in_file = example_data(...)

```python
in_file = example_data('TI4D.nii.gz')
```

**Verification:**
```python
assert fit_qt1_3.cmdline == expected_cmd
```

### Step 5: Assign fit_qt1.inputs.source_file = in_file

```python
fit_qt1.inputs.source_file = in_file
```

### Step 6: Assign cmd_tmp = '{cmd} -source {in_file} -comp {comp} -error {error} -m0map {map0} -mcmap {cmap} -res {res} -syn {syn} -t1map {t1map}'

```python
cmd_tmp = '{cmd} -source {in_file} -comp {comp} -error {error} -m0map {map0} -mcmap {cmap} -res {res} -syn {syn} -t1map {t1map}'
```

### Step 7: Assign expected_cmd = cmd_tmp.format(...)

```python
expected_cmd = cmd_tmp.format(cmd=cmd, in_file=in_file, comp='TI4D_comp.nii.gz', map0='TI4D_m0map.nii.gz', error='TI4D_error.nii.gz', cmap='TI4D_mcmap.nii.gz', res='TI4D_res.nii.gz', t1map='TI4D_t1map.nii.gz', syn='TI4D_syn.nii.gz')
```

**Verification:**
```python
assert fit_qt1.cmdline == expected_cmd
```

### Step 8: Assign fit_qt1_2 = FitQt1(...)

```python
fit_qt1_2 = FitQt1(tis=[1, 2, 5], ir_flag=True)
```

### Step 9: Assign in_file = example_data(...)

```python
in_file = example_data('TI4D.nii.gz')
```

### Step 10: Assign fit_qt1_2.inputs.source_file = in_file

```python
fit_qt1_2.inputs.source_file = in_file
```

### Step 11: Assign cmd_tmp = '{cmd} -source {in_file} -IR -TIs 1.0 2.0 5.0 -comp {comp} -error {error} -m0map {map0} -mcmap {cmap} -res {res} -syn {syn} -t1map {t1map}'

```python
cmd_tmp = '{cmd} -source {in_file} -IR -TIs 1.0 2.0 5.0 -comp {comp} -error {error} -m0map {map0} -mcmap {cmap} -res {res} -syn {syn} -t1map {t1map}'
```

### Step 12: Assign expected_cmd = cmd_tmp.format(...)

```python
expected_cmd = cmd_tmp.format(cmd=cmd, in_file=in_file, comp='TI4D_comp.nii.gz', map0='TI4D_m0map.nii.gz', error='TI4D_error.nii.gz', cmap='TI4D_mcmap.nii.gz', res='TI4D_res.nii.gz', t1map='TI4D_t1map.nii.gz', syn='TI4D_syn.nii.gz')
```

**Verification:**
```python
assert fit_qt1_2.cmdline == expected_cmd
```

### Step 13: Assign fit_qt1_3 = FitQt1(...)

```python
fit_qt1_3 = FitQt1(flips=[2, 4, 8], spgr=True)
```

### Step 14: Assign in_file = example_data(...)

```python
in_file = example_data('TI4D.nii.gz')
```

### Step 15: Assign fit_qt1_3.inputs.source_file = in_file

```python
fit_qt1_3.inputs.source_file = in_file
```

### Step 16: Assign cmd_tmp = '{cmd} -source {in_file} -comp {comp} -error {error} -flips 2.0 4.0 8.0 -m0map {map0} -mcmap {cmap} -res {res} -SPGR -syn {syn} -t1map {t1map}'

```python
cmd_tmp = '{cmd} -source {in_file} -comp {comp} -error {error} -flips 2.0 4.0 8.0 -m0map {map0} -mcmap {cmap} -res {res} -SPGR -syn {syn} -t1map {t1map}'
```

### Step 17: Assign expected_cmd = cmd_tmp.format(...)

```python
expected_cmd = cmd_tmp.format(cmd=cmd, in_file=in_file, comp='TI4D_comp.nii.gz', map0='TI4D_m0map.nii.gz', error='TI4D_error.nii.gz', cmap='TI4D_mcmap.nii.gz', res='TI4D_res.nii.gz', t1map='TI4D_t1map.nii.gz', syn='TI4D_syn.nii.gz')
```

**Verification:**
```python
assert fit_qt1_3.cmdline == expected_cmd
```

### Step 18: Call fit_qt1.run()

```python
fit_qt1.run()
```


## Complete Example

```python
# Workflow
'Testing FitQt1 interface.'
fit_qt1 = FitQt1()
cmd = get_custom_path('fit_qt1', env_dir='NIFTYFITDIR')
assert fit_qt1.cmd == cmd
with pytest.raises(ValueError):
    fit_qt1.run()
in_file = example_data('TI4D.nii.gz')
fit_qt1.inputs.source_file = in_file
cmd_tmp = '{cmd} -source {in_file} -comp {comp} -error {error} -m0map {map0} -mcmap {cmap} -res {res} -syn {syn} -t1map {t1map}'
expected_cmd = cmd_tmp.format(cmd=cmd, in_file=in_file, comp='TI4D_comp.nii.gz', map0='TI4D_m0map.nii.gz', error='TI4D_error.nii.gz', cmap='TI4D_mcmap.nii.gz', res='TI4D_res.nii.gz', t1map='TI4D_t1map.nii.gz', syn='TI4D_syn.nii.gz')
assert fit_qt1.cmdline == expected_cmd
fit_qt1_2 = FitQt1(tis=[1, 2, 5], ir_flag=True)
in_file = example_data('TI4D.nii.gz')
fit_qt1_2.inputs.source_file = in_file
cmd_tmp = '{cmd} -source {in_file} -IR -TIs 1.0 2.0 5.0 -comp {comp} -error {error} -m0map {map0} -mcmap {cmap} -res {res} -syn {syn} -t1map {t1map}'
expected_cmd = cmd_tmp.format(cmd=cmd, in_file=in_file, comp='TI4D_comp.nii.gz', map0='TI4D_m0map.nii.gz', error='TI4D_error.nii.gz', cmap='TI4D_mcmap.nii.gz', res='TI4D_res.nii.gz', t1map='TI4D_t1map.nii.gz', syn='TI4D_syn.nii.gz')
assert fit_qt1_2.cmdline == expected_cmd
fit_qt1_3 = FitQt1(flips=[2, 4, 8], spgr=True)
in_file = example_data('TI4D.nii.gz')
fit_qt1_3.inputs.source_file = in_file
cmd_tmp = '{cmd} -source {in_file} -comp {comp} -error {error} -flips 2.0 4.0 8.0 -m0map {map0} -mcmap {cmap} -res {res} -SPGR -syn {syn} -t1map {t1map}'
expected_cmd = cmd_tmp.format(cmd=cmd, in_file=in_file, comp='TI4D_comp.nii.gz', map0='TI4D_m0map.nii.gz', error='TI4D_error.nii.gz', cmap='TI4D_mcmap.nii.gz', res='TI4D_res.nii.gz', t1map='TI4D_t1map.nii.gz', syn='TI4D_syn.nii.gz')
assert fit_qt1_3.cmdline == expected_cmd
```

## Next Steps


---

*Source: test_qt1.py:13 | Complexity: Advanced | Last updated: 2026-05-18*