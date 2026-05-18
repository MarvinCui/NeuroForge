# How To: Project Onto Surface

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test _project_onto_surface (gh-10930).

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.channels`
- `mne.datasets`
- `mne.io`
- `mne.surface`
- `mne.transforms`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: method, ret_nn
```

## Step-by-Step Guide

### Step 1: 'Test _project_onto_surface (gh-10930).'

```python
'Test _project_onto_surface (gh-10930).'
```

**Verification:**
```python
assert len(surf['rr']) == 642
```

### Step 2: Assign locs = np.random.default_rng.normal(...)

```python
locs = np.random.default_rng(0).normal(size=(10, 3))
```

**Verification:**
```python
assert_allclose(np.linalg.norm(surf['rr'], axis=1), 1.0, rtol=0.001)
```

### Step 3: Assign surf = _get_ico_surface(...)

```python
surf = _get_ico_surface(3)
```

**Verification:**
```python
assert_allclose(np.linalg.norm(locs, axis=1), 1.0, rtol=1e-05)
```

### Step 4: Call assert_allclose()

```python
assert_allclose(np.linalg.norm(surf['rr'], axis=1), 1.0, rtol=0.001)
```

**Verification:**
```python
assert len(out) == 2 if ret_nn else 1
```

### Step 5: Assign unknown = _project_onto_surface(...)

```python
weights, tri_idx, *out = _project_onto_surface(locs, surf, project_rrs=True, return_nn=ret_nn, method=method)
```

**Verification:**
```python
assert_allclose(np.linalg.norm(comp, axis=1), 1.0, atol=0.05, err_msg=f'{kind} not unit vectors for {method}')
```

### Step 6: Call assert_allclose()

```python
assert_allclose(np.linalg.norm(locs, axis=1), 1.0, rtol=1e-05)
```

**Verification:**
```python
assert_allclose(cos, 1.0, atol=0.05, err_msg=f'{kind} not in same direction as locs for {method}')
```

### Step 7: Call assert_allclose()

```python
assert_allclose(np.linalg.norm(comp, axis=1), 1.0, atol=0.05, err_msg=f'{kind} not unit vectors for {method}')
```

### Step 8: Assign cos = np.sum(...)

```python
cos = np.sum(locs * comp, axis=1)
```

### Step 9: Call assert_allclose()

```python
assert_allclose(cos, 1.0, atol=0.05, err_msg=f'{kind} not in same direction as locs for {method}')
```


## Complete Example

```python
# Setup
# Fixtures: method, ret_nn

# Workflow
'Test _project_onto_surface (gh-10930).'
locs = np.random.default_rng(0).normal(size=(10, 3))
locs *= 2 / np.linalg.norm(locs, axis=1)[:, None]
surf = _get_ico_surface(3)
assert len(surf['rr']) == 642
assert_allclose(np.linalg.norm(surf['rr'], axis=1), 1.0, rtol=0.001)
weights, tri_idx, *out = _project_onto_surface(locs, surf, project_rrs=True, return_nn=ret_nn, method=method)
locs /= 2.0
assert_allclose(np.linalg.norm(locs, axis=1), 1.0, rtol=1e-05)
assert len(out) == 2 if ret_nn else 1
for kind, comp in zip(('rr', 'nn'), out):
    assert_allclose(np.linalg.norm(comp, axis=1), 1.0, atol=0.05, err_msg=f'{kind} not unit vectors for {method}')
    cos = np.sum(locs * comp, axis=1)
    assert_allclose(cos, 1.0, atol=0.05, err_msg=f'{kind} not in same direction as locs for {method}')
```

## Next Steps


---

*Source: test_surface.py:340 | Complexity: Advanced | Last updated: 2026-05-18*