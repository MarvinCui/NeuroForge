# How To: Laplacianthickness Wrongargs

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test LaplacianThickness wrongargs

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `segmentation`
- `test_resampling`
- `os`
- `pytest`

**Setup Required:**
```python
# Fixtures: change_dir, create_lt
```

## Step-by-Step Guide

### Step 1: Assign lt = create_lt

```python
lt = create_lt
```

**Verification:**
```python
assert lt.cmdline == 'LaplacianThickness functional.nii diffusion_weighted.nii functional_thickness.nii 4.5 5.9 0.01 0.15 0.001'
```

### Step 2: Assign lt.inputs.tolerance = 0.001

```python
lt.inputs.tolerance = 0.001
```

### Step 3: Assign lt.inputs.sulcus_prior = 0.15

```python
lt.inputs.sulcus_prior = 0.15
```

### Step 4: Assign lt.inputs.dT = 0.01

```python
lt.inputs.dT = 0.01
```

### Step 5: Assign lt.inputs.prior_thickness = 5.9

```python
lt.inputs.prior_thickness = 5.9
```

### Step 6: Assign lt.inputs.smooth_param = 4.5

```python
lt.inputs.smooth_param = 4.5
```

**Verification:**
```python
assert lt.cmdline == 'LaplacianThickness functional.nii diffusion_weighted.nii functional_thickness.nii 4.5 5.9 0.01 0.15 0.001'
```

### Step 7: lt.cmdline

```python
lt.cmdline
```

### Step 8: lt.cmdline

```python
lt.cmdline
```

### Step 9: lt.cmdline

```python
lt.cmdline
```

### Step 10: lt.cmdline

```python
lt.cmdline
```


## Complete Example

```python
# Setup
# Fixtures: change_dir, create_lt

# Workflow
lt = create_lt
lt.inputs.tolerance = 0.001
with pytest.raises(ValueError, match=".* requires a value for input 'sulcus_prior' .*"):
    lt.cmdline
lt.inputs.sulcus_prior = 0.15
with pytest.raises(ValueError, match=".* requires a value for input 'dT' .*"):
    lt.cmdline
lt.inputs.dT = 0.01
with pytest.raises(ValueError, match=".* requires a value for input 'prior_thickness' .*"):
    lt.cmdline
lt.inputs.prior_thickness = 5.9
with pytest.raises(ValueError, match=".* requires a value for input 'smooth_param' .*"):
    lt.cmdline
lt.inputs.smooth_param = 4.5
assert lt.cmdline == 'LaplacianThickness functional.nii diffusion_weighted.nii functional_thickness.nii 4.5 5.9 0.01 0.15 0.001'
```

## Next Steps


---

*Source: test_segmentation.py:43 | Complexity: Advanced | Last updated: 2026-05-18*