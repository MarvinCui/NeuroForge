# How To: Process Clim Round Trip

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test basic input-output support.

## Prerequisites

**Required Modules:**
- `contextlib`
- `pathlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `matplotlib.colors`
- `matplotlib.figure`
- `numpy.testing`
- `mne`
- `mne._fiff._digitization`
- `mne._fiff.constants`
- `mne.bem`
- `mne.datasets`
- `mne.defaults`
- `mne.fixes`
- `mne.io`
- `mne.minimum_norm`
- `mne.source_estimate`
- `mne.source_space`
- `mne.transforms`
- `mne.utils`
- `mne.viz`
- `mne.viz._3d`
- `mne.viz.utils`
- `pytest`
- `mne`
- `mne.datasets`
- `mne.viz`


## Step-by-Step Guide

### Step 1: 'Test basic input-output support.'

```python
'Test basic input-output support.'
```

**Verification:**
```python
assert_allclose(ticks, [-1, 0, 1])
```

### Step 2: Assign out = _process_clim(...)

```python
out = _process_clim('auto', 'auto', True, -1.0)
```

**Verification:**
```python
assert_allclose(ticks, [1])
```

### Step 3: Assign want = dict(...)

```python
want = dict(colormap=mne_analyze_colormap([0, 0.5, 1], 'matplotlib'), clim=dict(kind='value', pos_lims=[1, 1, 1]), transparent=True)
```

**Verification:**
```python
assert_allclose(ticks, [-1, -0.5, 0, 0.5, 1])
```

### Step 4: Call _assert_mapdata_equal()

```python
_assert_mapdata_equal(out, want)
```

**Verification:**
```python
assert_allclose(ticks, [-1, -0.5, -0.25, 0, 0.25, 0.5, 1])
```

### Step 5: Assign out2 = _process_clim(...)

```python
out2 = _process_clim(**out)
```

### Step 6: Call _assert_mapdata_equal()

```python
_assert_mapdata_equal(out, out2)
```

### Step 7: Call _linearize_map()

```python
_linearize_map(out)
```

### Step 8: Assign ticks = _get_map_ticks(...)

```python
ticks = _get_map_ticks(out)
```

### Step 9: Call assert_allclose()

```python
assert_allclose(ticks, [-1, 0, 1])
```

### Step 10: Assign out = _process_clim(...)

```python
out = _process_clim('auto', 'auto', True, 1.0)
```

### Step 11: Assign want = dict(...)

```python
want = dict(colormap=_get_cmap('hot'), clim=dict(kind='value', lims=[1, 1, 1]), transparent=True)
```

### Step 12: Call _assert_mapdata_equal()

```python
_assert_mapdata_equal(out, want)
```

### Step 13: Assign out2 = _process_clim(...)

```python
out2 = _process_clim(**out)
```

### Step 14: Call _assert_mapdata_equal()

```python
_assert_mapdata_equal(out, out2)
```

### Step 15: Call _linearize_map()

```python
_linearize_map(out)
```

### Step 16: Assign ticks = _get_map_ticks(...)

```python
ticks = _get_map_ticks(out)
```

### Step 17: Call assert_allclose()

```python
assert_allclose(ticks, [1])
```

### Step 18: Assign clim = dict(...)

```python
clim = dict(kind='value', pos_lims=[0, 0.5, 1])
```

### Step 19: Assign out = _process_clim(...)

```python
out = _process_clim(clim, 'auto', True)
```

### Step 20: Assign want = dict(...)

```python
want = dict(colormap=mne_analyze_colormap([0, 0.5, 1], 'matplotlib'), clim=clim, transparent=True)
```

### Step 21: Call _assert_mapdata_equal()

```python
_assert_mapdata_equal(out, want)
```

### Step 22: Call _linearize_map()

```python
_linearize_map(out)
```

### Step 23: Assign ticks = _get_map_ticks(...)

```python
ticks = _get_map_ticks(out)
```

### Step 24: Call assert_allclose()

```python
assert_allclose(ticks, [-1, -0.5, 0, 0.5, 1])
```

### Step 25: Assign clim = dict(...)

```python
clim = dict(kind='value', pos_lims=[0.25, 0.5, 1])
```

### Step 26: Assign out = _process_clim(...)

```python
out = _process_clim(clim, 'auto', True)
```

### Step 27: Assign want = dict(...)

```python
want = dict(colormap=mne_analyze_colormap([0, 0.5, 1], 'matplotlib'), clim=clim, transparent=True)
```

### Step 28: Call _assert_mapdata_equal()

```python
_assert_mapdata_equal(out, want)
```

### Step 29: Call _linearize_map()

```python
_linearize_map(out)
```

### Step 30: Assign ticks = _get_map_ticks(...)

```python
ticks = _get_map_ticks(out)
```

### Step 31: Call assert_allclose()

```python
assert_allclose(ticks, [-1, -0.5, -0.25, 0, 0.25, 0.5, 1])
```


## Complete Example

```python
# Workflow
'Test basic input-output support.'
out = _process_clim('auto', 'auto', True, -1.0)
want = dict(colormap=mne_analyze_colormap([0, 0.5, 1], 'matplotlib'), clim=dict(kind='value', pos_lims=[1, 1, 1]), transparent=True)
_assert_mapdata_equal(out, want)
out2 = _process_clim(**out)
_assert_mapdata_equal(out, out2)
_linearize_map(out)
ticks = _get_map_ticks(out)
assert_allclose(ticks, [-1, 0, 1])
out = _process_clim('auto', 'auto', True, 1.0)
want = dict(colormap=_get_cmap('hot'), clim=dict(kind='value', lims=[1, 1, 1]), transparent=True)
_assert_mapdata_equal(out, want)
out2 = _process_clim(**out)
_assert_mapdata_equal(out, out2)
_linearize_map(out)
ticks = _get_map_ticks(out)
assert_allclose(ticks, [1])
clim = dict(kind='value', pos_lims=[0, 0.5, 1])
out = _process_clim(clim, 'auto', True)
want = dict(colormap=mne_analyze_colormap([0, 0.5, 1], 'matplotlib'), clim=clim, transparent=True)
_assert_mapdata_equal(out, want)
_linearize_map(out)
ticks = _get_map_ticks(out)
assert_allclose(ticks, [-1, -0.5, 0, 0.5, 1])
clim = dict(kind='value', pos_lims=[0.25, 0.5, 1])
out = _process_clim(clim, 'auto', True)
want = dict(colormap=mne_analyze_colormap([0, 0.5, 1], 'matplotlib'), clim=clim, transparent=True)
_assert_mapdata_equal(out, want)
_linearize_map(out)
ticks = _get_map_ticks(out)
assert_allclose(ticks, [-1, -0.5, -0.25, 0, 0.25, 0.5, 1])
```

## Next Steps


---

*Source: test_3d.py:1003 | Complexity: Advanced | Last updated: 2026-05-18*