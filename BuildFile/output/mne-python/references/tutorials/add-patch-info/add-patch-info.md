# How To: Add Patch Info

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: Test adding patch info to source space.

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
# Fixtures: monkeypatch
```

## Step-by-Step Guide

### Step 1: 'Test adding patch info to source space.'

```python
'Test adding patch info to source space.'
```

**Verification:**
```python
assert all((s['nearest'] is None for s in src_new))
```

### Step 2: Assign src = _read_small_src(...)

```python
src = _read_small_src(remove=False)
```

**Verification:**
```python
assert all((s['nearest_dist'] is None for s in src_new))
```

### Step 3: Assign src_new = _read_small_src(...)

```python
src_new = _read_small_src()
```

**Verification:**
```python
assert all((s['pinfo'] is None for s in src_new))
```

### Step 4: Call add_source_space_distances()

```python
add_source_space_distances(src_new, dist_limit=1e-05)
```

**Verification:**
```python
assert all((s['nearest'] is None for s in src_new))
```

### Step 5: Call _compare_source_spaces()

```python
_compare_source_spaces(src, src_new, 'approx')
```

### Step 6: Assign src_nodist = src.copy(...)

```python
src_nodist = src.copy()
```

### Step 7: Call add_source_space_distances()

```python
add_source_space_distances(src_new, dist_limit=0)
```

### Step 8: Call _compare_source_spaces()

```python
_compare_source_spaces(src, src_new, 'approx')
```

### Step 9: Call m.setattr()

```python
m.setattr(mne.source_space._source_space, '_DIST_WARN_LIMIT', 1)
```

### Step 10: Call add_source_space_distances()

```python
add_source_space_distances(src_new)
```

### Step 11: Assign unknown = None

```python
s[key] = None
```


## Complete Example

```python
# Setup
# Fixtures: monkeypatch

# Workflow
'Test adding patch info to source space.'
src = _read_small_src(remove=False)
src_new = _read_small_src()
add_source_space_distances(src_new, dist_limit=1e-05)
assert all((s['nearest'] is None for s in src_new))
assert all((s['nearest_dist'] is None for s in src_new))
assert all((s['pinfo'] is None for s in src_new))
with monkeypatch.context() as m:
    m.setattr(mne.source_space._source_space, '_DIST_WARN_LIMIT', 1)
    with pytest.warns(RuntimeWarning, match='Computing distances for 258'):
        add_source_space_distances(src_new)
_compare_source_spaces(src, src_new, 'approx')
src_nodist = src.copy()
for s in src_nodist:
    for key in ('dist', 'dist_limit'):
        s[key] = None
add_source_space_distances(src_new, dist_limit=0)
_compare_source_spaces(src, src_new, 'approx')
```

## Next Steps


---

*Source: test_source_space.py:137 | Complexity: Advanced | Last updated: 2026-05-18*