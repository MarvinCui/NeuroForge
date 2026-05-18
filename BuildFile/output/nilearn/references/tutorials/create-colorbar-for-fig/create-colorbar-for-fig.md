# How To: Create Colorbar For Fig

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test nilearn.plotting._engine_utils.create_colorbar_for_fig function for
valid values.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `re`
- `numpy`
- `pytest`
- `matplotlib.colors`
- `nilearn.plotting._engine_utils`

**Setup Required:**
```python
# Fixtures: matplotlib_pyplot, threshold, cbar_vmin, cbar_vmax, vmin, vmax, expected_ticks
```

## Step-by-Step Guide

### Step 1: 'Test nilearn.plotting._engine_utils.create_colorbar_for_fig function for\n    valid values.\n    '

```python
'Test nilearn.plotting._engine_utils.create_colorbar_for_fig function for\n    valid values.\n    '
```

**Verification:**
```python
assert colorbar is not None
```

### Step 2: Assign unknown = matplotlib_pyplot.subplots(...)

```python
fig, ax = matplotlib_pyplot.subplots()
```

**Verification:**
```python
assert [float(tick.get_text()) for tick in colorbar.ax.get_yticklabels()] == expected_ticks
```

### Step 3: Assign cmap = matplotlib_pyplot.get_cmap(...)

```python
cmap = matplotlib_pyplot.get_cmap('Greys')
```

### Step 4: Assign norm = Normalize(...)

```python
norm = Normalize(vmin, vmax)
```

### Step 5: Assign colorbar = create_colorbar_for_fig(...)

```python
colorbar = create_colorbar_for_fig(fig, ax, cmap, norm, threshold, cbar_vmin, cbar_vmax)
```

**Verification:**
```python
assert colorbar is not None
```


## Complete Example

```python
# Setup
# Fixtures: matplotlib_pyplot, threshold, cbar_vmin, cbar_vmax, vmin, vmax, expected_ticks

# Workflow
'Test nilearn.plotting._engine_utils.create_colorbar_for_fig function for\n    valid values.\n    '
fig, ax = matplotlib_pyplot.subplots()
cmap = matplotlib_pyplot.get_cmap('Greys')
norm = Normalize(vmin, vmax)
colorbar = create_colorbar_for_fig(fig, ax, cmap, norm, threshold, cbar_vmin, cbar_vmax)
assert colorbar is not None
assert [float(tick.get_text()) for tick in colorbar.ax.get_yticklabels()] == expected_ticks
```

## Next Steps


---

*Source: test_engine_utils.py:174 | Complexity: Intermediate | Last updated: 2026-05-18*