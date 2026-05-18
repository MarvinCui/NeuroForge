# How To: Convert Forward

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test converting forward solution between different representations.

## Prerequisites

**Required Modules:**
- `gc`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.pick`
- `mne.channels`
- `mne.datasets`
- `mne.forward`
- `mne.io`
- `mne.label`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test converting forward solution between different representations.'

```python
'Test converting forward solution between different representations.'
```

**Verification:**
```python
assert '306' in fwd_repr
```

### Step 2: Assign fwd = read_forward_solution(...)

```python
fwd = read_forward_solution(fname_meeg_grad)
```

**Verification:**
```python
assert '60' in fwd_repr
```

### Step 3: Assign fwd_repr = repr(...)

```python
fwd_repr = repr(fwd)
```

**Verification:**
```python
assert fwd_repr
```

### Step 4: Assign fwd_surf = convert_forward_solution(...)

```python
fwd_surf = convert_forward_solution(fwd, surf_ori=True)
```

**Verification:**
```python
assert isinstance(fwd, Forward)
```

### Step 5: Assign fwd_new = convert_forward_solution(...)

```python
fwd_new = convert_forward_solution(fwd_surf, surf_ori=False)
```

**Verification:**
```python
assert repr(fwd_new)
```

### Step 6: Call assert_forward_allclose()

```python
assert_forward_allclose(fwd, fwd_new)
```

**Verification:**
```python
assert isinstance(fwd_new, Forward)
```

### Step 7: Call gc.collect()

```python
gc.collect()
```

**Verification:**
```python
assert_forward_allclose(fwd, fwd_new)
```

### Step 8: Assign fwd_fixed = convert_forward_solution(...)

```python
fwd_fixed = convert_forward_solution(fwd_surf, surf_ori=True, force_fixed=True, use_cps=False)
```

**Verification:**
```python
assert repr(fwd_fixed)
```

### Step 9: Call gc.collect()

```python
gc.collect()
```

**Verification:**
```python
assert isinstance(fwd_fixed, Forward)
```

### Step 10: Assign fwd_new = convert_forward_solution(...)

```python
fwd_new = convert_forward_solution(fwd_fixed, surf_ori=False, force_fixed=False)
```

**Verification:**
```python
assert is_fixed_orient(fwd_fixed)
```

### Step 11: Call assert_forward_allclose()

```python
assert_forward_allclose(fwd, fwd_new)
```

**Verification:**
```python
assert repr(fwd_new)
```

### Step 12: Call gc.collect()

```python
gc.collect()
```

**Verification:**
```python
assert isinstance(fwd_new, Forward)
```


## Complete Example

```python
# Workflow
'Test converting forward solution between different representations.'
fwd = read_forward_solution(fname_meeg_grad)
fwd_repr = repr(fwd)
assert '306' in fwd_repr
assert '60' in fwd_repr
assert fwd_repr
assert isinstance(fwd, Forward)
fwd_surf = convert_forward_solution(fwd, surf_ori=True)
fwd_new = convert_forward_solution(fwd_surf, surf_ori=False)
assert repr(fwd_new)
assert isinstance(fwd_new, Forward)
assert_forward_allclose(fwd, fwd_new)
del fwd_new
gc.collect()
fwd_fixed = convert_forward_solution(fwd_surf, surf_ori=True, force_fixed=True, use_cps=False)
del fwd_surf
gc.collect()
assert repr(fwd_fixed)
assert isinstance(fwd_fixed, Forward)
assert is_fixed_orient(fwd_fixed)
fwd_new = convert_forward_solution(fwd_fixed, surf_ori=False, force_fixed=False)
assert repr(fwd_new)
assert isinstance(fwd_new, Forward)
assert_forward_allclose(fwd, fwd_new)
del fwd, fwd_new, fwd_fixed
gc.collect()
```

## Next Steps


---

*Source: test_forward.py:72 | Complexity: Advanced | Last updated: 2026-05-18*