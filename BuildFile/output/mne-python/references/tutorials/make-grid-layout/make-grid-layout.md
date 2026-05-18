# How To: Make Grid Layout

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test creation of grid layout.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `copy`
- `pathlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.meas_info`
- `mne.channels`
- `mne.channels.layout`
- `mne.defaults`
- `mne.io`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test creation of grid layout.'

```python
'Test creation of grid layout.'
```

**Verification:**
```python
assert_array_equal(lout_new.kind, 'bar')
```

### Step 2: Assign lout_orig = read_layout(...)

```python
lout_orig = read_layout(fname=lout_path / 'test_ica.lout')
```

**Verification:**
```python
assert_array_equal(lout_orig.pos, lout_new.pos)
```

### Step 3: Assign layout = make_grid_layout(...)

```python
layout = make_grid_layout(_get_test_info())
```

**Verification:**
```python
assert_array_equal(lout_orig.names, lout_new.names)
```

### Step 4: Call layout.save()

```python
layout.save(str(tmp_path / 'bar.lout'))
```

**Verification:**
```python
assert layout.pos[0, 1] == layout.pos[1, 1]
```

### Step 5: Assign lout_new = read_layout(...)

```python
lout_new = read_layout(fname=tmp_path / 'bar.lout')
```

**Verification:**
```python
assert layout.pos[0, 0] != layout.pos[1, 0]
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(lout_new.kind, 'bar')
```

**Verification:**
```python
assert_array_equal(layout.pos[0, 3:], layout.pos[1, 3:])
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(lout_orig.pos, lout_new.pos)
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(lout_orig.names, lout_new.names)
```

### Step 9: Assign layout = make_grid_layout(...)

```python
layout = make_grid_layout(_get_test_info(), n_col=2)
```

**Verification:**
```python
assert layout.pos[0, 1] == layout.pos[1, 1]
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(layout.pos[0, 3:], layout.pos[1, 3:])
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test creation of grid layout.'
lout_orig = read_layout(fname=lout_path / 'test_ica.lout')
layout = make_grid_layout(_get_test_info())
layout.save(str(tmp_path / 'bar.lout'))
lout_new = read_layout(fname=tmp_path / 'bar.lout')
assert_array_equal(lout_new.kind, 'bar')
assert_array_equal(lout_orig.pos, lout_new.pos)
assert_array_equal(lout_orig.names, lout_new.names)
layout = make_grid_layout(_get_test_info(), n_col=2)
assert layout.pos[0, 1] == layout.pos[1, 1]
assert layout.pos[0, 0] != layout.pos[1, 0]
assert_array_equal(layout.pos[0, 3:], layout.pos[1, 3:])
```

## Next Steps


---

*Source: test_layout.py:214 | Complexity: Advanced | Last updated: 2026-05-18*