# How To: Get Colormap From Array

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test setting a colormap.

## Prerequisites

**Required Modules:**
- `platform`
- `colorsys`
- `numpy`
- `pytest`
- `mne`
- `mne.io`
- `mne.utils`
- `mne.viz.backends._utils`
- `matplotlib.colors`


## Step-by-Step Guide

### Step 1: 'Test setting a colormap.'

```python
'Test setting a colormap.'
```

**Verification:**
```python
assert isinstance(cmap, LinearSegmentedColormap)
```

### Step 2: Assign cmap = _get_colormap_from_array(...)

```python
cmap = _get_colormap_from_array()
```

**Verification:**
```python
assert isinstance(cmap, ListedColormap)
```

### Step 3: Assign cmap = _get_colormap_from_array(...)

```python
cmap = _get_colormap_from_array(colormap='viridis')
```

**Verification:**
```python
assert isinstance(cmap, ListedColormap)
```

### Step 4: Assign cmap = _get_colormap_from_array(...)

```python
cmap = _get_colormap_from_array(colormap=[1, 1, 1], normalized_colormap=True)
```

**Verification:**
```python
assert isinstance(cmap, ListedColormap)
```

### Step 5: Assign cmap = _get_colormap_from_array(...)

```python
cmap = _get_colormap_from_array(colormap=[255, 255, 255], normalized_colormap=False)
```

**Verification:**
```python
assert isinstance(cmap, ListedColormap)
```


## Complete Example

```python
# Workflow
'Test setting a colormap.'
from matplotlib.colors import LinearSegmentedColormap, ListedColormap
cmap = _get_colormap_from_array()
assert isinstance(cmap, LinearSegmentedColormap)
cmap = _get_colormap_from_array(colormap='viridis')
assert isinstance(cmap, ListedColormap)
cmap = _get_colormap_from_array(colormap=[1, 1, 1], normalized_colormap=True)
assert isinstance(cmap, ListedColormap)
cmap = _get_colormap_from_array(colormap=[255, 255, 255], normalized_colormap=False)
assert isinstance(cmap, ListedColormap)
```

## Next Steps


---

*Source: test_utils.py:22 | Complexity: Intermediate | Last updated: 2026-05-18*