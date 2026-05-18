# How To: Randomise2

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test randomise2

## Prerequisites

**Required Modules:**
- `os`
- `nipype.interfaces.fsl.dti`
- `nipype.interfaces.fsl`
- `nipype.interfaces.base`
- `pytest`
- `nipype.testing.fixtures`


## Step-by-Step Guide

### Step 1: Assign rand = fsl.Randomise(...)

```python
rand = fsl.Randomise()
```

**Verification:**
```python
assert rand.cmd == 'randomise'
```

### Step 2: Assign rand.inputs.input_4D = 'infile.nii'

```python
rand.inputs.input_4D = 'infile.nii'
```

**Verification:**
```python
assert actualCmdline == desiredCmdline
```

### Step 3: Assign rand.inputs.output_rootname = 'outfile'

```python
rand.inputs.output_rootname = 'outfile'
```

**Verification:**
```python
assert actualCmdline == desiredCmdline
```

### Step 4: Assign rand.inputs.design_matrix = 'design.mat'

```python
rand.inputs.design_matrix = 'design.mat'
```

**Verification:**
```python
assert results.runtime.cmdline == 'randomise -i infile3 -o outfile3'
```

### Step 5: Assign rand.inputs.t_contrast = 'infile.con'

```python
rand.inputs.t_contrast = 'infile.con'
```

**Verification:**
```python
assert rand4.cmdline == rand4.cmd + ' -i infile -o root ' + settings[0]
```

### Step 6: Assign actualCmdline = sorted(...)

```python
actualCmdline = sorted(rand.cmdline.split())
```

### Step 7: Assign cmd = 'randomise -i infile.nii -o outfile -d design.mat -t infile.con'

```python
cmd = 'randomise -i infile.nii -o outfile -d design.mat -t infile.con'
```

### Step 8: Assign desiredCmdline = sorted(...)

```python
desiredCmdline = sorted(cmd.split())
```

**Verification:**
```python
assert actualCmdline == desiredCmdline
```

### Step 9: Assign rand2 = fsl.Randomise(...)

```python
rand2 = fsl.Randomise(input_4D='infile2', output_rootname='outfile2', f_contrast='infile.f', one_sample_gmean=True, int_seed=4)
```

### Step 10: Assign actualCmdline = sorted(...)

```python
actualCmdline = sorted(rand2.cmdline.split())
```

### Step 11: Assign cmd = 'randomise -i infile2 -o outfile2 -1 -f infile.f --seed=4'

```python
cmd = 'randomise -i infile2 -o outfile2 -1 -f infile.f --seed=4'
```

### Step 12: Assign desiredCmdline = sorted(...)

```python
desiredCmdline = sorted(cmd.split())
```

**Verification:**
```python
assert actualCmdline == desiredCmdline
```

### Step 13: Assign rand3 = fsl.Randomise(...)

```python
rand3 = fsl.Randomise()
```

### Step 14: Assign results = rand3.run(...)

```python
results = rand3.run(input_4D='infile3', output_rootname='outfile3')
```

**Verification:**
```python
assert results.runtime.cmdline == 'randomise -i infile3 -o outfile3'
```

### Step 15: Assign opt_map = value

```python
opt_map = {'demean_data': ('-D', True), 'one_sample_gmean': ('-1', True), 'mask_image': ('-m inp_mask', 'inp_mask'), 'design_matrix': ('-d design.mat', 'design.mat'), 't_contrast': ('-t input.con', 'input.con'), 'f_contrast': ('-f input.fts', 'input.fts'), 'xchange_block_labels': ('-e design.grp', 'design.grp'), 'print_unique_perm': ('-q', True), 'print_info_parallelMode': ('-Q', True), 'num_permutations': ('-n 10', 10), 'vox_pvalus': ('-x', True), 'fstats_only': ('--fonly', True), 'thresh_free_cluster': ('-T', True), 'thresh_free_cluster_2Dopt': ('--T2', True), 'cluster_thresholding': ('-c 0.20', 0.2), 'cluster_mass_thresholding': ('-C 0.40', 0.4), 'fcluster_thresholding': ('-F 0.10', 0.1), 'fcluster_mass_thresholding': ('-S 0.30', 0.3), 'variance_smoothing': ('-v 0.20', 0.2), 'diagnostics_off': ('--quiet', True), 'output_raw': ('-R', True), 'output_perm_vect': ('-P', True), 'int_seed': ('--seed=20', 20), 'TFCE_height_param': ('--tfce_H=0.11', 0.11), 'TFCE_extent_param': ('--tfce_E=0.50', 0.5), 'TFCE_connectivity': ('--tfce_C=0.30', 0.3), 'list_num_voxel_EVs_pos': ('--vxl=1,2,3,4', '1,2,3,4'), 'list_img_voxel_EVs': ('--vxf=6,7,8,9,3', '6,7,8,9,3')}
```

### Step 16: Call rand.run()

```python
rand.run()
```

### Step 17: Assign rand4 = fsl.Randomise(...)

```python
rand4 = fsl.Randomise(input_4D='infile', output_rootname='root', **{name: settings[1]})
```

**Verification:**
```python
assert rand4.cmdline == rand4.cmd + ' -i infile -o root ' + settings[0]
```


## Complete Example

```python
# Workflow
rand = fsl.Randomise()
assert rand.cmd == 'randomise'
with pytest.raises(ValueError):
    rand.run()
rand.inputs.input_4D = 'infile.nii'
rand.inputs.output_rootname = 'outfile'
rand.inputs.design_matrix = 'design.mat'
rand.inputs.t_contrast = 'infile.con'
actualCmdline = sorted(rand.cmdline.split())
cmd = 'randomise -i infile.nii -o outfile -d design.mat -t infile.con'
desiredCmdline = sorted(cmd.split())
assert actualCmdline == desiredCmdline
rand2 = fsl.Randomise(input_4D='infile2', output_rootname='outfile2', f_contrast='infile.f', one_sample_gmean=True, int_seed=4)
actualCmdline = sorted(rand2.cmdline.split())
cmd = 'randomise -i infile2 -o outfile2 -1 -f infile.f --seed=4'
desiredCmdline = sorted(cmd.split())
assert actualCmdline == desiredCmdline
rand3 = fsl.Randomise()
results = rand3.run(input_4D='infile3', output_rootname='outfile3')
assert results.runtime.cmdline == 'randomise -i infile3 -o outfile3'
opt_map = {'demean_data': ('-D', True), 'one_sample_gmean': ('-1', True), 'mask_image': ('-m inp_mask', 'inp_mask'), 'design_matrix': ('-d design.mat', 'design.mat'), 't_contrast': ('-t input.con', 'input.con'), 'f_contrast': ('-f input.fts', 'input.fts'), 'xchange_block_labels': ('-e design.grp', 'design.grp'), 'print_unique_perm': ('-q', True), 'print_info_parallelMode': ('-Q', True), 'num_permutations': ('-n 10', 10), 'vox_pvalus': ('-x', True), 'fstats_only': ('--fonly', True), 'thresh_free_cluster': ('-T', True), 'thresh_free_cluster_2Dopt': ('--T2', True), 'cluster_thresholding': ('-c 0.20', 0.2), 'cluster_mass_thresholding': ('-C 0.40', 0.4), 'fcluster_thresholding': ('-F 0.10', 0.1), 'fcluster_mass_thresholding': ('-S 0.30', 0.3), 'variance_smoothing': ('-v 0.20', 0.2), 'diagnostics_off': ('--quiet', True), 'output_raw': ('-R', True), 'output_perm_vect': ('-P', True), 'int_seed': ('--seed=20', 20), 'TFCE_height_param': ('--tfce_H=0.11', 0.11), 'TFCE_extent_param': ('--tfce_E=0.50', 0.5), 'TFCE_connectivity': ('--tfce_C=0.30', 0.3), 'list_num_voxel_EVs_pos': ('--vxl=1,2,3,4', '1,2,3,4'), 'list_img_voxel_EVs': ('--vxf=6,7,8,9,3', '6,7,8,9,3')}
for name, settings in list(opt_map.items()):
    rand4 = fsl.Randomise(input_4D='infile', output_rootname='root', **{name: settings[1]})
    assert rand4.cmdline == rand4.cmd + ' -i infile -o root ' + settings[0]
```

## Next Steps


---

*Source: test_dti.py:42 | Complexity: Advanced | Last updated: 2026-05-18*