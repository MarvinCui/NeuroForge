# How To: Surface Source Space Doc

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: mock, pytest, workflow, integration

## Overview

Workflow: Test surface source space docstring.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.pick`
- `mne.datasets`
- `mne.fixes`
- `mne.source_estimate`
- `mne.source_space`
- `mne.source_space._source_space`
- `mne.surface`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: src_kind
```

## Step-by-Step Guide

### Step 1: 'Test surface source space docstring.'

```python
'Test surface source space docstring.'
```

**Verification:**
```python
assert src_kind == 'src'
```

### Step 2: Assign src = mne.read_source_spaces(...)

```python
src = mne.read_source_spaces(fname_fwd)
```

**Verification:**
```python
assert len(s['pinfo']) == s['nuse']
```

### Step 3: Assign src = mne.read_source_spaces(...)

```python
src = mne.read_source_spaces(fname_src)
```

**Verification:**
```python
assert_array_equal(s['patch_inds'], np.arange(s['nuse']))
```

### Step 4: Assign all_pinfo = np.concatenate(...)

```python
all_pinfo = np.concatenate(s['pinfo'])
```

**Verification:**
```python
assert len(s['pinfo']) > s['nuse']
```

### Step 5: Call assert_array_equal()

```python
assert_array_equal(np.sort(all_pinfo), np.arange(s['np']))
```

**Verification:**
```python
assert_array_equal(np.sort(all_pinfo), np.arange(s['np']))
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(s['patch_inds'], np.arange(s['nuse']))
```

**Verification:**
```python
assert len(s['patch_inds']) == s['nuse']
```

### Step 7: Assign this_dense_vertex = value

```python
this_dense_vertex = s['vertno'][idx]
```

**Verification:**
```python
assert len(s['vertno']) == s['nuse']
```

### Step 8: Assign this_vertex_represents = value

```python
this_vertex_represents = s['pinfo'][s['patch_inds'][idx]]
```

**Verification:**
```python
assert len(s['patch_inds']) == s['nuse']
```


## Complete Example

```python
# Setup
# Fixtures: src_kind

# Workflow
'Test surface source space docstring.'
if src_kind == 'fwd':
    src = mne.read_source_spaces(fname_fwd)
else:
    assert src_kind == 'src'
    src = mne.read_source_spaces(fname_src)
for s in src:
    if src_kind == 'src':
        assert len(s['pinfo']) == s['nuse']
        assert_array_equal(s['patch_inds'], np.arange(s['nuse']))
    else:
        assert len(s['pinfo']) > s['nuse']
    all_pinfo = np.concatenate(s['pinfo'])
    assert_array_equal(np.sort(all_pinfo), np.arange(s['np']))
    assert len(s['patch_inds']) == s['nuse']
    assert len(s['vertno']) == s['nuse']
    assert len(s['patch_inds']) == s['nuse']
    for idx in (0, 42, 173):
        this_dense_vertex = s['vertno'][idx]
        this_vertex_represents = s['pinfo'][s['patch_inds'][idx]]
        assert len(this_vertex_represents) > 1
        for other in this_vertex_represents:
            assert s['nearest'][other] == this_dense_vertex
```

## Next Steps


---

*Source: test_source_space.py:168 | Complexity: Advanced | Last updated: 2026-05-18*