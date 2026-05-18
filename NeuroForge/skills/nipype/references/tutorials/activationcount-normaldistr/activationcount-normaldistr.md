# How To: Activationcount Normaldistr

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test ActivationCount normaldistr

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `nibabel`
- `nipype.algorithms.stats`
- `pytest`

**Setup Required:**
```python
# Fixtures: tmpdir, threshold, above_thresh
```

## Step-by-Step Guide

### Step 1: Call tmpdir.chdir()

```python
tmpdir.chdir()
```

**Verification:**
```python
assert np.isclose(pos.get_fdata().mean(), above_thresh * 0.01, rtol=0.1, atol=0.0001)
```

### Step 2: Assign in_files = value

```python
in_files = [f'{i:d}.nii' for i in range(3)]
```

**Verification:**
```python
assert np.isclose(neg.get_fdata().mean(), above_thresh * 0.01, rtol=0.1, atol=0.0001)
```

### Step 3: Assign acm = ActivationCount(...)

```python
acm = ActivationCount(in_files=in_files, threshold=threshold)
```

### Step 4: Assign res = acm.run(...)

```python
res = acm.run()
```

### Step 5: Assign pos = nb.load(...)

```python
pos = nb.load(res.outputs.acm_pos)
```

### Step 6: Assign neg = nb.load(...)

```python
neg = nb.load(res.outputs.acm_neg)
```

**Verification:**
```python
assert np.isclose(pos.get_fdata().mean(), above_thresh * 0.01, rtol=0.1, atol=0.0001)
```

### Step 7: Call nb.Nifti1Image.to_filename()

```python
nb.Nifti1Image(np.random.normal(size=(100, 100, 100)), np.eye(4)).to_filename(fname)
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir, threshold, above_thresh

# Workflow
tmpdir.chdir()
in_files = [f'{i:d}.nii' for i in range(3)]
for fname in in_files:
    nb.Nifti1Image(np.random.normal(size=(100, 100, 100)), np.eye(4)).to_filename(fname)
acm = ActivationCount(in_files=in_files, threshold=threshold)
res = acm.run()
pos = nb.load(res.outputs.acm_pos)
neg = nb.load(res.outputs.acm_neg)
assert np.isclose(pos.get_fdata().mean(), above_thresh * 0.01, rtol=0.1, atol=0.0001)
assert np.isclose(neg.get_fdata().mean(), above_thresh * 0.01, rtol=0.1, atol=0.0001)
```

## Next Steps


---

*Source: test_stats.py:32 | Complexity: Intermediate | Last updated: 2026-05-18*