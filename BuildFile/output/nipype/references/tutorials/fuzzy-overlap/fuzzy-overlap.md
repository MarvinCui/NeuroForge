# How To: Fuzzy Overlap

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test fuzzy overlap

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `nibabel`
- `nipype.testing`
- `metrics`

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
assert out.dice == 1
```

### Step 2: Assign in_mask = example_data(...)

```python
in_mask = example_data('tpms_msk.nii.gz')
```

**Verification:**
```python
assert out.dice == 1
```

### Step 3: Assign tpms = value

```python
tpms = [example_data('tpm_%02d.nii.gz' % i) for i in range(3)]
```

**Verification:**
```python
assert 0 < out.dice < 1
```

### Step 4: Assign out = value

```python
out = FuzzyOverlap(in_ref=tpms[0], in_tst=tpms[0]).run().outputs
```

**Verification:**
```python
assert out.dice == 1.0
```

### Step 5: Assign out = value

```python
out = FuzzyOverlap(in_mask=in_mask, in_ref=tpms[0], in_tst=tpms[0]).run().outputs
```

**Verification:**
```python
assert out.dice == 1.0
```

### Step 6: Assign out = value

```python
out = FuzzyOverlap(in_mask=in_mask, in_ref=tpms[0], in_tst=tpms[1]).run().outputs
```

**Verification:**
```python
assert np.allclose(out.dice, 0.82051)
```

### Step 7: Assign out = value

```python
out = FuzzyOverlap(in_ref=tpms, in_tst=tpms).run().outputs
```

**Verification:**
```python
assert np.allclose(out.dice, 0.74074)
```

### Step 8: Assign out = value

```python
out = FuzzyOverlap(in_mask=in_mask, in_ref=tpms, in_tst=tpms).run().outputs
```

**Verification:**
```python
assert out.dice == 1.0
```

### Step 9: Assign data = np.zeros(...)

```python
data = np.zeros((3, 3, 3), dtype=float)
```

### Step 10: Assign unknown = 0.5

```python
data[0, 0, 0] = 0.5
```

### Step 11: Assign unknown = 0.25

```python
data[2, 2, 2] = 0.25
```

### Step 12: Assign unknown = 0.3

```python
data[1, 1, 1] = 0.3
```

### Step 13: Call nb.Nifti1Image.to_filename()

```python
nb.Nifti1Image(data, np.eye(4)).to_filename('test1.nii.gz')
```

### Step 14: Assign data = np.zeros(...)

```python
data = np.zeros((3, 3, 3), dtype=float)
```

### Step 15: Assign unknown = 0.6

```python
data[0, 0, 0] = 0.6
```

### Step 16: Assign unknown = 0.3

```python
data[1, 1, 1] = 0.3
```

### Step 17: Call nb.Nifti1Image.to_filename()

```python
nb.Nifti1Image(data, np.eye(4)).to_filename('test2.nii.gz')
```

### Step 18: Assign out = value

```python
out = FuzzyOverlap(in_ref='test1.nii.gz', in_tst='test2.nii.gz').run().outputs
```

**Verification:**
```python
assert np.allclose(out.dice, 0.82051)
```

### Step 19: Assign data = np.zeros(...)

```python
data = np.zeros((3, 3, 3), dtype=np.uint8)
```

### Step 20: Assign unknown = 1

```python
data[0, 0, 0] = 1
```

### Step 21: Assign unknown = 1

```python
data[2, 2, 2] = 1
```

### Step 22: Call nb.Nifti1Image.to_filename()

```python
nb.Nifti1Image(data, np.eye(4)).to_filename('mask.nii.gz')
```

### Step 23: Assign out = value

```python
out = FuzzyOverlap(in_ref='test1.nii.gz', in_tst='test2.nii.gz', in_mask='mask.nii.gz').run().outputs
```

**Verification:**
```python
assert np.allclose(out.dice, 0.74074)
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
tmpdir.chdir()
in_mask = example_data('tpms_msk.nii.gz')
tpms = [example_data('tpm_%02d.nii.gz' % i) for i in range(3)]
out = FuzzyOverlap(in_ref=tpms[0], in_tst=tpms[0]).run().outputs
assert out.dice == 1
out = FuzzyOverlap(in_mask=in_mask, in_ref=tpms[0], in_tst=tpms[0]).run().outputs
assert out.dice == 1
out = FuzzyOverlap(in_mask=in_mask, in_ref=tpms[0], in_tst=tpms[1]).run().outputs
assert 0 < out.dice < 1
out = FuzzyOverlap(in_ref=tpms, in_tst=tpms).run().outputs
assert out.dice == 1.0
out = FuzzyOverlap(in_mask=in_mask, in_ref=tpms, in_tst=tpms).run().outputs
assert out.dice == 1.0
data = np.zeros((3, 3, 3), dtype=float)
data[0, 0, 0] = 0.5
data[2, 2, 2] = 0.25
data[1, 1, 1] = 0.3
nb.Nifti1Image(data, np.eye(4)).to_filename('test1.nii.gz')
data = np.zeros((3, 3, 3), dtype=float)
data[0, 0, 0] = 0.6
data[1, 1, 1] = 0.3
nb.Nifti1Image(data, np.eye(4)).to_filename('test2.nii.gz')
out = FuzzyOverlap(in_ref='test1.nii.gz', in_tst='test2.nii.gz').run().outputs
assert np.allclose(out.dice, 0.82051)
data = np.zeros((3, 3, 3), dtype=np.uint8)
data[0, 0, 0] = 1
data[2, 2, 2] = 1
nb.Nifti1Image(data, np.eye(4)).to_filename('mask.nii.gz')
out = FuzzyOverlap(in_ref='test1.nii.gz', in_tst='test2.nii.gz', in_mask='mask.nii.gz').run().outputs
assert np.allclose(out.dice, 0.74074)
```

## Next Steps


---

*Source: test_metrics.py:10 | Complexity: Advanced | Last updated: 2026-05-18*