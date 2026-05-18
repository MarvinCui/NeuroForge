# How To: Fslrmsdeviation

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test FSLRMSDeviation

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
assert np.allclose(orig.values, derived.values, equal_nan=True, atol=0.0001)
```

### Step 2: Assign xfms = value

```python
xfms = data_dir / f'{base}_from-orig_to-boldref_mode-image_desc-hmc_xfm.txt'
```

### Step 3: Assign boldref = value

```python
boldref = data_dir / f'{base}_desc-hmc_boldref.nii.gz'
```

### Step 4: Assign timeseries = value

```python
timeseries = data_dir / f'{base}_desc-motion_timeseries.tsv'
```

### Step 5: Assign rmsd = pe.Node(...)

```python
rmsd = pe.Node(confounds.FSLRMSDeviation(xfm_file=str(xfms), boldref_file=str(boldref)), name='rmsd', base_dir=str(tmp_path))
```

### Step 6: Assign res = rmsd.run(...)

```python
res = rmsd.run()
```

### Step 7: Assign orig = value

```python
orig = pd.read_csv(timeseries, sep='\t')['rmsd']
```

### Step 8: Assign derived = value

```python
derived = pd.read_csv(res.outputs.out_file, sep='\t')['rmsd']
```

**Verification:**
```python
assert np.allclose(orig.values, derived.values, equal_nan=True, atol=0.0001)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, data_dir

# Workflow
base = 'sub-01_task-mixedgamblestask_run-01'
xfms = data_dir / f'{base}_from-orig_to-boldref_mode-image_desc-hmc_xfm.txt'
boldref = data_dir / f'{base}_desc-hmc_boldref.nii.gz'
timeseries = data_dir / f'{base}_desc-motion_timeseries.tsv'
rmsd = pe.Node(confounds.FSLRMSDeviation(xfm_file=str(xfms), boldref_file=str(boldref)), name='rmsd', base_dir=str(tmp_path))
res = rmsd.run()
orig = pd.read_csv(timeseries, sep='\t')['rmsd']
derived = pd.read_csv(res.outputs.out_file, sep='\t')['rmsd']
assert np.allclose(orig.values, derived.values, equal_nan=True, atol=0.0001)
```

## Next Steps


---

*Source: test_confounds.py:36 | Complexity: Advanced | Last updated: 2026-05-18*