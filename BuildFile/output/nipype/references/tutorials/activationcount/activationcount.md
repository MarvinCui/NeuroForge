# How To: Activationcount

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test ActivationCount

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `nibabel`
- `nipype.algorithms.stats`
- `pytest`

**Setup Required:**
```python
# Fixtures: tmpdir
```

## Step-by-Step Guide

### Step 1: Call tmpdir.chdir()

```python
tmpdir.chdir()
```

**Verification:**
```python
assert np.allclose(diff.get_fdata(), pos.get_fdata() - neg.get_fdata())
```

### Step 2: Assign in_files = value

```python
in_files = [f'{i:d}.nii' for i in range(3)]
```

### Step 3: Assign acm = ActivationCount(...)

```python
acm = ActivationCount(in_files=in_files, threshold=1.65)
```

### Step 4: Assign res = acm.run(...)

```python
res = acm.run()
```

### Step 5: Assign diff = nb.load(...)

```python
diff = nb.load(res.outputs.out_file)
```

### Step 6: Assign pos = nb.load(...)

```python
pos = nb.load(res.outputs.acm_pos)
```

### Step 7: Assign neg = nb.load(...)

```python
neg = nb.load(res.outputs.acm_neg)
```

**Verification:**
```python
assert np.allclose(diff.get_fdata(), pos.get_fdata() - neg.get_fdata())
```

### Step 8: Call nb.Nifti1Image.to_filename()

```python
nb.Nifti1Image(np.random.normal(size=(5, 5, 5)), np.eye(4)).to_filename(fname)
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
tmpdir.chdir()
in_files = [f'{i:d}.nii' for i in range(3)]
for fname in in_files:
    nb.Nifti1Image(np.random.normal(size=(5, 5, 5)), np.eye(4)).to_filename(fname)
acm = ActivationCount(in_files=in_files, threshold=1.65)
res = acm.run()
diff = nb.load(res.outputs.out_file)
pos = nb.load(res.outputs.acm_pos)
neg = nb.load(res.outputs.acm_neg)
assert np.allclose(diff.get_fdata(), pos.get_fdata() - neg.get_fdata())
```

## Next Steps


---

*Source: test_stats.py:10 | Complexity: Advanced | Last updated: 2026-05-18*