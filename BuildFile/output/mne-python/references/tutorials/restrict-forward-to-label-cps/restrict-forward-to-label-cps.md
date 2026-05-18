# How To: Restrict Forward To Label Cps

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test for gh-11689.

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: tmp_path, use_cps
```

## Step-by-Step Guide

### Step 1: 'Test for gh-11689.'

```python
'Test for gh-11689.'
```

**Verification:**
```python
assert fwd['surf_ori']
```

### Step 2: Assign label_lh = read_label(...)

```python
label_lh = read_label(label_path / 'Aud-lh.label')
```

**Verification:**
```python
assert not is_fixed_orient(fwd)
```

### Step 3: Assign fwd = read_forward_solution(...)

```python
fwd = read_forward_solution(fname_meeg)
```

**Verification:**
```python
assert idx == 126
```

### Step 4: Call convert_forward_solution()

```python
convert_forward_solution(fwd, surf_ori=True, force_fixed=False, copy=False, use_cps=use_cps)
```

**Verification:**
```python
assert fwd_out['surf_ori']
```

### Step 5: Assign fwd = pick_types_forward(...)

```python
fwd = pick_types_forward(fwd, meg='mag')
```

**Verification:**
```python
assert not is_fixed_orient(fwd_out)
```

### Step 6: Assign fwd_out = restrict_forward_to_label(...)

```python
fwd_out = restrict_forward_to_label(fwd, label_lh)
```

**Verification:**
```python
assert idx == 0
```

### Step 7: Assign vert = value

```python
vert = fwd_out['src'][0]['vertno'][0]
```

**Verification:**
```python
assert_allclose(go2, go1)
```

### Step 8: Assign idx = list.index(...)

```python
idx = list(fwd['src'][0]['vertno']).index(vert)
```

**Verification:**
```python
assert_allclose(gs2, gs1)
```

### Step 9: Assign go1 = unknown.copy(...)

```python
go1 = fwd['_orig_sol'][:, idx * 3:idx * 3 + 3].copy()
```

**Verification:**
```python
assert fwd_out['surf_ori']
```

### Step 10: Assign gs1 = unknown.copy(...)

```python
gs1 = fwd['sol']['data'][:, idx * 3:idx * 3 + 3].copy()
```

**Verification:**
```python
assert not is_fixed_orient(fwd_out)
```

### Step 11: Assign idx = list.index(...)

```python
idx = list(fwd_out['src'][0]['vertno']).index(vert)
```

**Verification:**
```python
assert list(fwd_out['src'][0]['vertno']).index(vert) == 0
```

### Step 12: Assign go2 = unknown.copy(...)

```python
go2 = fwd_out['_orig_sol'][:, idx * 3:idx * 3 + 3].copy()
```

**Verification:**
```python
assert_allclose(go3, go1)
```

### Step 13: Assign gs2 = unknown.copy(...)

```python
gs2 = fwd_out['sol']['data'][:, idx * 3:idx * 3 + 3].copy()
```

**Verification:**
```python
assert_allclose(gs3, gs1)
```

### Step 14: Call assert_allclose()

```python
assert_allclose(go2, go1)
```

### Step 15: Call assert_allclose()

```python
assert_allclose(gs2, gs1)
```

### Step 16: Call convert_forward_solution()

```python
convert_forward_solution(fwd_out, surf_ori=True, force_fixed=False, copy=False, use_cps=use_cps)
```

**Verification:**
```python
assert fwd_out['surf_ori']
```

### Step 17: Assign go3 = unknown.copy(...)

```python
go3 = fwd_out['_orig_sol'][:, idx * 3:idx * 3 + 3].copy()
```

### Step 18: Assign gs3 = unknown.copy(...)

```python
gs3 = fwd_out['sol']['data'][:, idx * 3:idx * 3 + 3].copy()
```

### Step 19: Call assert_allclose()

```python
assert_allclose(go3, go1)
```

### Step 20: Call assert_allclose()

```python
assert_allclose(gs3, gs1)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, use_cps

# Workflow
'Test for gh-11689.'
label_lh = read_label(label_path / 'Aud-lh.label')
fwd = read_forward_solution(fname_meeg)
convert_forward_solution(fwd, surf_ori=True, force_fixed=False, copy=False, use_cps=use_cps)
fwd = pick_types_forward(fwd, meg='mag')
fwd_out = restrict_forward_to_label(fwd, label_lh)
vert = fwd_out['src'][0]['vertno'][0]
assert fwd['surf_ori']
assert not is_fixed_orient(fwd)
idx = list(fwd['src'][0]['vertno']).index(vert)
assert idx == 126
go1 = fwd['_orig_sol'][:, idx * 3:idx * 3 + 3].copy()
gs1 = fwd['sol']['data'][:, idx * 3:idx * 3 + 3].copy()
assert fwd_out['surf_ori']
assert not is_fixed_orient(fwd_out)
idx = list(fwd_out['src'][0]['vertno']).index(vert)
assert idx == 0
go2 = fwd_out['_orig_sol'][:, idx * 3:idx * 3 + 3].copy()
gs2 = fwd_out['sol']['data'][:, idx * 3:idx * 3 + 3].copy()
assert_allclose(go2, go1)
assert_allclose(gs2, gs1)
convert_forward_solution(fwd_out, surf_ori=True, force_fixed=False, copy=False, use_cps=use_cps)
assert fwd_out['surf_ori']
assert not is_fixed_orient(fwd_out)
assert list(fwd_out['src'][0]['vertno']).index(vert) == 0
go3 = fwd_out['_orig_sol'][:, idx * 3:idx * 3 + 3].copy()
gs3 = fwd_out['sol']['data'][:, idx * 3:idx * 3 + 3].copy()
assert_allclose(go3, go1)
assert_allclose(gs3, gs1)
```

## Next Steps


---

*Source: test_forward.py:395 | Complexity: Advanced | Last updated: 2026-05-18*