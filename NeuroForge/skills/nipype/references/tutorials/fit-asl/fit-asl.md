# How To: Fit Asl

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Testing FitAsl interface.

## Prerequisites

**Required Modules:**
- `pytest`
- `testing`
- `niftyreg`
- `asl`
- `niftyreg.tests.test_regutils`


## Step-by-Step Guide

### Step 1: 'Testing FitAsl interface.'

```python
'Testing FitAsl interface.'
```

**Verification:**
```python
assert fit_asl.cmd == cmd
```

### Step 2: Assign fit_asl = FitAsl(...)

```python
fit_asl = FitAsl()
```

**Verification:**
```python
assert fit_asl.cmdline == expected_cmd
```

### Step 3: Assign cmd = get_custom_path(...)

```python
cmd = get_custom_path('fit_asl', env_dir='NIFTYFIT_DIR')
```

**Verification:**
```python
assert fit_asl2.cmdline == expected_cmd
```

### Step 4: Assign in_file = example_data(...)

```python
in_file = example_data('asl.nii.gz')
```

### Step 5: Assign fit_asl.inputs.source_file = in_file

```python
fit_asl.inputs.source_file = in_file
```

### Step 6: Assign cmd_tmp = '{cmd} -source {in_file} -cbf {cbf} -error {error} -syn {syn}'

```python
cmd_tmp = '{cmd} -source {in_file} -cbf {cbf} -error {error} -syn {syn}'
```

### Step 7: Assign expected_cmd = cmd_tmp.format(...)

```python
expected_cmd = cmd_tmp.format(cmd=cmd, in_file=in_file, cbf='asl_cbf.nii.gz', error='asl_error.nii.gz', syn='asl_syn.nii.gz')
```

**Verification:**
```python
assert fit_asl.cmdline == expected_cmd
```

### Step 8: Assign fit_asl2 = FitAsl(...)

```python
fit_asl2 = FitAsl(sig=True)
```

### Step 9: Assign in_file = example_data(...)

```python
in_file = example_data('asl.nii.gz')
```

### Step 10: Assign t1map = example_data(...)

```python
t1map = example_data('T1map.nii.gz')
```

### Step 11: Assign seg = example_data(...)

```python
seg = example_data('segmentation0.nii.gz')
```

### Step 12: Assign fit_asl2.inputs.source_file = in_file

```python
fit_asl2.inputs.source_file = in_file
```

### Step 13: Assign fit_asl2.inputs.t1map = t1map

```python
fit_asl2.inputs.t1map = t1map
```

### Step 14: Assign fit_asl2.inputs.seg = seg

```python
fit_asl2.inputs.seg = seg
```

### Step 15: Assign cmd_tmp = '{cmd} -source {in_file} -cbf {cbf} -error {error} -seg {seg} -sig -syn {syn} -t1map {t1map}'

```python
cmd_tmp = '{cmd} -source {in_file} -cbf {cbf} -error {error} -seg {seg} -sig -syn {syn} -t1map {t1map}'
```

### Step 16: Assign expected_cmd = cmd_tmp.format(...)

```python
expected_cmd = cmd_tmp.format(cmd=cmd, in_file=in_file, t1map=t1map, seg=seg, cbf='asl_cbf.nii.gz', error='asl_error.nii.gz', syn='asl_syn.nii.gz')
```

**Verification:**
```python
assert fit_asl2.cmdline == expected_cmd
```

### Step 17: Call fit_asl.run()

```python
fit_asl.run()
```


## Complete Example

```python
# Workflow
'Testing FitAsl interface.'
fit_asl = FitAsl()
cmd = get_custom_path('fit_asl', env_dir='NIFTYFIT_DIR')
assert fit_asl.cmd == cmd
with pytest.raises(ValueError):
    fit_asl.run()
in_file = example_data('asl.nii.gz')
fit_asl.inputs.source_file = in_file
cmd_tmp = '{cmd} -source {in_file} -cbf {cbf} -error {error} -syn {syn}'
expected_cmd = cmd_tmp.format(cmd=cmd, in_file=in_file, cbf='asl_cbf.nii.gz', error='asl_error.nii.gz', syn='asl_syn.nii.gz')
assert fit_asl.cmdline == expected_cmd
fit_asl2 = FitAsl(sig=True)
in_file = example_data('asl.nii.gz')
t1map = example_data('T1map.nii.gz')
seg = example_data('segmentation0.nii.gz')
fit_asl2.inputs.source_file = in_file
fit_asl2.inputs.t1map = t1map
fit_asl2.inputs.seg = seg
cmd_tmp = '{cmd} -source {in_file} -cbf {cbf} -error {error} -seg {seg} -sig -syn {syn} -t1map {t1map}'
expected_cmd = cmd_tmp.format(cmd=cmd, in_file=in_file, t1map=t1map, seg=seg, cbf='asl_cbf.nii.gz', error='asl_error.nii.gz', syn='asl_syn.nii.gz')
assert fit_asl2.cmdline == expected_cmd
```

## Next Steps


---

*Source: test_asl.py:14 | Complexity: Advanced | Last updated: 2026-05-18*