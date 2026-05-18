# How To: Fslmotionparams

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test FSLMotionParams

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pandas`
- `nipype.pipeline`
- `fmriprep.interfaces`

**Setup Required:**
```python
# Fixtures: tmp_path, data_dir
```

## Step-by-Step Guide

### Step 1: Assign base = 'sub-01_task-mixedgamblestask_run-01'

```python
base = 'sub-01_task-mixedgamblestask_run-01'
```

**Verification:**
```python
assert np.all(max_diff < limits)
```

### Step 2: Assign xfms = value

```python
xfms = data_dir / f'{base}_from-orig_to-boldref_mode-image_desc-hmc_xfm.txt'
```

### Step 3: Assign boldref = value

```python
boldref = data_dir / f'{base}_desc-hmc_boldref.nii.gz'
```

### Step 4: Assign orig_timeseries = value

```python
orig_timeseries = data_dir / f'{base}_desc-motion_timeseries.tsv'
```

### Step 5: Assign motion = pe.Node(...)

```python
motion = pe.Node(confounds.FSLMotionParams(xfm_file=str(xfms), boldref_file=str(boldref)), name='fsl_motion', base_dir=str(tmp_path))
```

### Step 6: Assign res = motion.run(...)

```python
res = motion.run()
```

### Step 7: Assign derived_params = pd.read_csv(...)

```python
derived_params = pd.read_csv(res.outputs.out_file, sep='\t')
```

### Step 8: Assign orig_params = value

```python
orig_params = pd.read_csv(orig_timeseries, sep='\t')[derived_params.columns]
```

### Step 9: Assign limits = pd.DataFrame(...)

```python
limits = pd.DataFrame({'trans_x': [0.0001], 'trans_y': [0.0001], 'trans_z': [0.0001], 'rot_x': [1e-06], 'rot_y': [1e-06], 'rot_z': [1e-06]})
```

### Step 10: Assign max_diff = unknown.abs.max(...)

```python
max_diff = (orig_params - derived_params).abs().max()
```

**Verification:**
```python
assert np.all(max_diff < limits)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, data_dir

# Workflow
base = 'sub-01_task-mixedgamblestask_run-01'
xfms = data_dir / f'{base}_from-orig_to-boldref_mode-image_desc-hmc_xfm.txt'
boldref = data_dir / f'{base}_desc-hmc_boldref.nii.gz'
orig_timeseries = data_dir / f'{base}_desc-motion_timeseries.tsv'
motion = pe.Node(confounds.FSLMotionParams(xfm_file=str(xfms), boldref_file=str(boldref)), name='fsl_motion', base_dir=str(tmp_path))
res = motion.run()
derived_params = pd.read_csv(res.outputs.out_file, sep='\t')
orig_params = pd.read_csv(orig_timeseries, sep='\t')[derived_params.columns]
limits = pd.DataFrame({'trans_x': [0.0001], 'trans_y': [0.0001], 'trans_z': [0.0001], 'rot_x': [1e-06], 'rot_y': [1e-06], 'rot_z': [1e-06]})
max_diff = (orig_params - derived_params).abs().max()
assert np.all(max_diff < limits)
```

## Next Steps


---

*Source: test_confounds.py:56 | Complexity: Advanced | Last updated: 2026-05-18*