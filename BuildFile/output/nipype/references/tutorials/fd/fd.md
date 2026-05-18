# How To: Fd

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test fd

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

### Step 1: Assign tempdir = value

```python
tempdir = tmpdir.strpath
```

**Verification:**
```python
assert 'FramewiseDisplacement' in line
```

### Step 2: Assign ground_truth = np.loadtxt(...)

```python
ground_truth = np.loadtxt(example_data('fsl_motion_outliers_fd.txt'))
```

**Verification:**
```python
assert np.allclose(ground_truth, np.loadtxt(res.outputs.out_file, skiprows=1), atol=0.16)
```

### Step 3: Assign fdisplacement = FramewiseDisplacement(...)

```python
fdisplacement = FramewiseDisplacement(in_file=example_data('fsl_mcflirt_movpar.txt'), out_file=tempdir + '/fd.txt', parameter_source='FSL')
```

**Verification:**
```python
assert np.abs(ground_truth.mean() - res.outputs.fd_average) < 0.01
```

### Step 4: Assign res = fdisplacement.run(...)

```python
res = fdisplacement.run()
```

**Verification:**
```python
assert np.allclose(ground_truth, np.loadtxt(res.outputs.out_file, skiprows=1), atol=0.16)
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
tempdir = tmpdir.strpath
ground_truth = np.loadtxt(example_data('fsl_motion_outliers_fd.txt'))
fdisplacement = FramewiseDisplacement(in_file=example_data('fsl_mcflirt_movpar.txt'), out_file=tempdir + '/fd.txt', parameter_source='FSL')
res = fdisplacement.run()
with open(res.outputs.out_file) as all_lines:
    for line in all_lines:
        assert 'FramewiseDisplacement' in line
        break
assert np.allclose(ground_truth, np.loadtxt(res.outputs.out_file, skiprows=1), atol=0.16)
assert np.abs(ground_truth.mean() - res.outputs.fd_average) < 0.01
```

## Next Steps


---

*Source: test_confounds.py:17 | Complexity: Intermediate | Last updated: 2026-05-18*