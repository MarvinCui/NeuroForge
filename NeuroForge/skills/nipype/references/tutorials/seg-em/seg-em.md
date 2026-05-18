# How To: Seg Em

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test seg em

## Prerequisites

**Required Modules:**
- `pytest`
- `testing`
- `niftyreg`
- `niftyreg.tests.test_regutils`


## Step-by-Step Guide

### Step 1: Assign seg_em = EM(...)

```python
seg_em = EM()
```

**Verification:**
```python
assert seg_em.cmd == cmd
```

### Step 2: Assign cmd = get_custom_path(...)

```python
cmd = get_custom_path('seg_EM', env_dir='NIFTYSEGDIR')
```

**Verification:**
```python
assert seg_em.cmdline == expected_cmd
```

### Step 3: Assign in_file = example_data(...)

```python
in_file = example_data('im1.nii')
```

### Step 4: Assign seg_em.inputs.in_file = in_file

```python
seg_em.inputs.in_file = in_file
```

### Step 5: Assign seg_em.inputs.no_prior = 4

```python
seg_em.inputs.no_prior = 4
```

### Step 6: Assign cmd_tmp = '{cmd} -in {in_file} -nopriors 4 -bc_out {bc_out} -out {out_file} -out_outlier {out_outlier}'

```python
cmd_tmp = '{cmd} -in {in_file} -nopriors 4 -bc_out {bc_out} -out {out_file} -out_outlier {out_outlier}'
```

### Step 7: Assign expected_cmd = cmd_tmp.format(...)

```python
expected_cmd = cmd_tmp.format(cmd=cmd, in_file=in_file, out_file='im1_em.nii.gz', bc_out='im1_bc_em.nii.gz', out_outlier='im1_outlier_em.nii.gz')
```

**Verification:**
```python
assert seg_em.cmdline == expected_cmd
```

### Step 8: Call seg_em.run()

```python
seg_em.run()
```


## Complete Example

```python
# Workflow
seg_em = EM()
cmd = get_custom_path('seg_EM', env_dir='NIFTYSEGDIR')
assert seg_em.cmd == cmd
with pytest.raises(ValueError):
    seg_em.run()
in_file = example_data('im1.nii')
seg_em.inputs.in_file = in_file
seg_em.inputs.no_prior = 4
cmd_tmp = '{cmd} -in {in_file} -nopriors 4 -bc_out {bc_out} -out {out_file} -out_outlier {out_outlier}'
expected_cmd = cmd_tmp.format(cmd=cmd, in_file=in_file, out_file='im1_em.nii.gz', bc_out='im1_bc_em.nii.gz', out_outlier='im1_outlier_em.nii.gz')
assert seg_em.cmdline == expected_cmd
```

## Next Steps


---

*Source: test_em_interfaces.py:13 | Complexity: Advanced | Last updated: 2026-05-18*