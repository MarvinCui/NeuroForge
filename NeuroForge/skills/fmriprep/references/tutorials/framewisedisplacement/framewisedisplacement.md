# How To: Framewisedisplacement

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test FramewiseDisplacement

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

### Step 1: Assign timeseries = value

```python
timeseries = data_dir / 'sub-01_task-mixedgamblestask_run-01_desc-motion_timeseries.tsv'
```

**Verification:**
```python
assert np.allclose(orig.values, derived.values, equal_nan=True)
```

### Step 2: Assign framewise_displacement = pe.Node(...)

```python
framewise_displacement = pe.Node(confounds.FramewiseDisplacement(in_file=str(timeseries)), name='framewise_displacement', base_dir=str(tmp_path))
```

### Step 3: Assign res = framewise_displacement.run(...)

```python
res = framewise_displacement.run()
```

### Step 4: Assign orig = value

```python
orig = pd.read_csv(timeseries, sep='\t')['framewise_displacement']
```

### Step 5: Assign derived = value

```python
derived = pd.read_csv(res.outputs.out_file, sep='\t')['FramewiseDisplacement']
```

**Verification:**
```python
assert np.allclose(orig.values, derived.values, equal_nan=True)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, data_dir

# Workflow
timeseries = data_dir / 'sub-01_task-mixedgamblestask_run-01_desc-motion_timeseries.tsv'
framewise_displacement = pe.Node(confounds.FramewiseDisplacement(in_file=str(timeseries)), name='framewise_displacement', base_dir=str(tmp_path))
res = framewise_displacement.run()
orig = pd.read_csv(timeseries, sep='\t')['framewise_displacement']
derived = pd.read_csv(res.outputs.out_file, sep='\t')['FramewiseDisplacement']
assert np.allclose(orig.values, derived.values, equal_nan=True)
```

## Next Steps


---

*Source: test_confounds.py:90 | Complexity: Intermediate | Last updated: 2026-05-18*