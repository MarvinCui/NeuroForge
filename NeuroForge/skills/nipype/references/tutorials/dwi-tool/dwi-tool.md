# How To: Dwi Tool

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Testing DwiTool interface.

## Prerequisites

**Required Modules:**
- `pytest`
- `testing`
- `niftyreg`
- `dwi`
- `niftyreg.tests.test_regutils`


## Step-by-Step Guide

### Step 1: 'Testing DwiTool interface.'

```python
'Testing DwiTool interface.'
```

**Verification:**
```python
assert dwi_tool.cmd == cmd
```

### Step 2: Assign dwi_tool = DwiTool(...)

```python
dwi_tool = DwiTool()
```

**Verification:**
```python
assert dwi_tool.cmdline == expected_cmd
```

### Step 3: Assign cmd = get_custom_path(...)

```python
cmd = get_custom_path('dwi_tool', env_dir='NIFTYFITDIR')
```

**Verification:**
```python
assert dwi_tool.cmd == cmd
```

### Step 4: Assign in_file = example_data(...)

```python
in_file = example_data('dwi.nii.gz')
```

### Step 5: Assign bval_file = example_data(...)

```python
bval_file = example_data('bvals')
```

### Step 6: Assign bvec_file = example_data(...)

```python
bvec_file = example_data('bvecs')
```

### Step 7: Assign b0_file = example_data(...)

```python
b0_file = example_data('b0.nii')
```

### Step 8: Assign mask_file = example_data(...)

```python
mask_file = example_data('mask.nii.gz')
```

### Step 9: Assign dwi_tool.inputs.source_file = in_file

```python
dwi_tool.inputs.source_file = in_file
```

### Step 10: Assign dwi_tool.inputs.mask_file = mask_file

```python
dwi_tool.inputs.mask_file = mask_file
```

### Step 11: Assign dwi_tool.inputs.bval_file = bval_file

```python
dwi_tool.inputs.bval_file = bval_file
```

### Step 12: Assign dwi_tool.inputs.bvec_file = bvec_file

```python
dwi_tool.inputs.bvec_file = bvec_file
```

### Step 13: Assign dwi_tool.inputs.b0_file = b0_file

```python
dwi_tool.inputs.b0_file = b0_file
```

### Step 14: Assign dwi_tool.inputs.dti_flag = True

```python
dwi_tool.inputs.dti_flag = True
```

### Step 15: Assign cmd_tmp = '{cmd} -source {in_file} -bval {bval} -bvec {bvec} -b0 {b0} -mask {mask} -dti -famap {fa} -logdti2 {log} -mcmap {mc} -mdmap {md} -rgbmap {rgb} -syn {syn} -v1map {v1}'

```python
cmd_tmp = '{cmd} -source {in_file} -bval {bval} -bvec {bvec} -b0 {b0} -mask {mask} -dti -famap {fa} -logdti2 {log} -mcmap {mc} -mdmap {md} -rgbmap {rgb} -syn {syn} -v1map {v1}'
```

### Step 16: Assign expected_cmd = cmd_tmp.format(...)

```python
expected_cmd = cmd_tmp.format(cmd=cmd, in_file=in_file, bval=bval_file, bvec=bvec_file, b0=b0_file, mask=mask_file, fa='dwi_famap.nii.gz', log='dwi_logdti2.nii.gz', mc='dwi_mcmap.nii.gz', md='dwi_mdmap.nii.gz', rgb='dwi_rgbmap.nii.gz', syn='dwi_syn.nii.gz', v1='dwi_v1map.nii.gz')
```

**Verification:**
```python
assert dwi_tool.cmdline == expected_cmd
```

### Step 17: Call dwi_tool.run()

```python
dwi_tool.run()
```


## Complete Example

```python
# Workflow
'Testing DwiTool interface.'
dwi_tool = DwiTool()
cmd = get_custom_path('dwi_tool', env_dir='NIFTYFITDIR')
assert dwi_tool.cmd == cmd
with pytest.raises(ValueError):
    dwi_tool.run()
in_file = example_data('dwi.nii.gz')
bval_file = example_data('bvals')
bvec_file = example_data('bvecs')
b0_file = example_data('b0.nii')
mask_file = example_data('mask.nii.gz')
dwi_tool.inputs.source_file = in_file
dwi_tool.inputs.mask_file = mask_file
dwi_tool.inputs.bval_file = bval_file
dwi_tool.inputs.bvec_file = bvec_file
dwi_tool.inputs.b0_file = b0_file
dwi_tool.inputs.dti_flag = True
cmd_tmp = '{cmd} -source {in_file} -bval {bval} -bvec {bvec} -b0 {b0} -mask {mask} -dti -famap {fa} -logdti2 {log} -mcmap {mc} -mdmap {md} -rgbmap {rgb} -syn {syn} -v1map {v1}'
expected_cmd = cmd_tmp.format(cmd=cmd, in_file=in_file, bval=bval_file, bvec=bvec_file, b0=b0_file, mask=mask_file, fa='dwi_famap.nii.gz', log='dwi_logdti2.nii.gz', mc='dwi_mcmap.nii.gz', md='dwi_mdmap.nii.gz', rgb='dwi_rgbmap.nii.gz', syn='dwi_syn.nii.gz', v1='dwi_v1map.nii.gz')
assert dwi_tool.cmdline == expected_cmd
```

## Next Steps


---

*Source: test_dwi.py:62 | Complexity: Advanced | Last updated: 2026-05-18*