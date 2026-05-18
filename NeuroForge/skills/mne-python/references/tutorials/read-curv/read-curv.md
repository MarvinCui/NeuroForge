# How To: Read Curv

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test reading curvature data.

## Prerequisites

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


## Step-by-Step Guide

### Step 1: 'Test reading curvature data.'

```python
'Test reading curvature data.'
```

**Verification:**
```python
assert len(bin_curv) == len(rr)
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('nibabel')
```

**Verification:**
```python
assert np.logical_or(bin_curv == 0, bin_curv == 1).all()
```

### Step 3: Assign fname_curv = value

```python
fname_curv = data_path / 'subjects' / 'fsaverage' / 'surf' / 'lh.curv'
```

### Step 4: Assign fname_surf = value

```python
fname_surf = data_path / 'subjects' / 'fsaverage' / 'surf' / 'lh.inflated'
```

### Step 5: Assign bin_curv = read_curvature(...)

```python
bin_curv = read_curvature(fname_curv)
```

### Step 6: Assign rr = value

```python
rr = read_surface(fname_surf)[0]
```

**Verification:**
```python
assert len(bin_curv) == len(rr)
```


## Complete Example

```python
# Workflow
'Test reading curvature data.'
pytest.importorskip('nibabel')
fname_curv = data_path / 'subjects' / 'fsaverage' / 'surf' / 'lh.curv'
fname_surf = data_path / 'subjects' / 'fsaverage' / 'surf' / 'lh.inflated'
bin_curv = read_curvature(fname_curv)
rr = read_surface(fname_surf)[0]
assert len(bin_curv) == len(rr)
assert np.logical_or(bin_curv == 0, bin_curv == 1).all()
```

## Next Steps


---

*Source: test_surface.py:159 | Complexity: Intermediate | Last updated: 2026-05-18*