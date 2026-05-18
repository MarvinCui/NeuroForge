# How To: Dvars

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test dvars

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pytest`
- `nipype.testing`
- `nipype.algorithms.confounds`
- `numpy`
- `nitime`

**Setup Required:**
```python
# Fixtures: tmpdir
```

## Step-by-Step Guide

### Step 1: Assign ground_truth = np.loadtxt(...)

```python
ground_truth = np.loadtxt(example_data('ds003_sub-01_mc.DVARS'))
```

**Verification:**
```python
assert np.abs(dv1[:, 0] - ground_truth[:, 0]).sum() / len(dv1) < 0.05
```

### Step 2: Assign dvars = ComputeDVARS(...)

```python
dvars = ComputeDVARS(in_file=example_data('ds003_sub-01_mc.nii.gz'), in_mask=example_data('ds003_sub-01_mc_brainmask.nii.gz'), save_all=True, intensity_normalization=0)
```

**Verification:**
```python
assert np.abs(dv1[:, 1] - ground_truth[:, 1]).sum() / len(dv1) < 0.05
```

### Step 3: Call tmpdir.chdir()

```python
tmpdir.chdir()
```

**Verification:**
```python
assert np.abs(dv1[:, 2] - ground_truth[:, 2]).sum() / len(dv1) < 0.05
```

### Step 4: Assign res = dvars.run(...)

```python
res = dvars.run()
```

**Verification:**
```python
assert np.abs(dv1[:, 0] - ground_truth[:, 0]).sum() / len(dv1) < 0.05
```

### Step 5: Assign dv1 = np.loadtxt(...)

```python
dv1 = np.loadtxt(res.outputs.out_all, skiprows=1)
```

**Verification:**
```python
assert np.abs(dv1[:, 1] - ground_truth[:, 1]).sum() / len(dv1) > 0.05
```

### Step 6: Assign dvars = ComputeDVARS(...)

```python
dvars = ComputeDVARS(in_file=example_data('ds003_sub-01_mc.nii.gz'), in_mask=example_data('ds003_sub-01_mc_brainmask.nii.gz'), save_all=True)
```

**Verification:**
```python
assert np.abs(dv1[:, 2] - ground_truth[:, 2]).sum() / len(dv1) < 0.05
```

### Step 7: Assign res = dvars.run(...)

```python
res = dvars.run()
```

### Step 8: Assign dv1 = np.loadtxt(...)

```python
dv1 = np.loadtxt(res.outputs.out_all, skiprows=1)
```

**Verification:**
```python
assert np.abs(dv1[:, 0] - ground_truth[:, 0]).sum() / len(dv1) < 0.05
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
ground_truth = np.loadtxt(example_data('ds003_sub-01_mc.DVARS'))
dvars = ComputeDVARS(in_file=example_data('ds003_sub-01_mc.nii.gz'), in_mask=example_data('ds003_sub-01_mc_brainmask.nii.gz'), save_all=True, intensity_normalization=0)
tmpdir.chdir()
res = dvars.run()
dv1 = np.loadtxt(res.outputs.out_all, skiprows=1)
assert np.abs(dv1[:, 0] - ground_truth[:, 0]).sum() / len(dv1) < 0.05
assert np.abs(dv1[:, 1] - ground_truth[:, 1]).sum() / len(dv1) < 0.05
assert np.abs(dv1[:, 2] - ground_truth[:, 2]).sum() / len(dv1) < 0.05
dvars = ComputeDVARS(in_file=example_data('ds003_sub-01_mc.nii.gz'), in_mask=example_data('ds003_sub-01_mc_brainmask.nii.gz'), save_all=True)
res = dvars.run()
dv1 = np.loadtxt(res.outputs.out_all, skiprows=1)
assert np.abs(dv1[:, 0] - ground_truth[:, 0]).sum() / len(dv1) < 0.05
assert np.abs(dv1[:, 1] - ground_truth[:, 1]).sum() / len(dv1) > 0.05
assert np.abs(dv1[:, 2] - ground_truth[:, 2]).sum() / len(dv1) < 0.05
```

## Next Steps


---

*Source: test_confounds.py:39 | Complexity: Advanced | Last updated: 2026-05-18*