# How To: Plot Markers Node Sizes Lyrz Display

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Tests for plot_markers and 'lyrz' display mode.

Tests that markers are plotted with the requested size
with display_mode='lyrz'. (See issue #3012 and PR #3013).

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `nilearn.conftest`
- `nilearn.plotting`

**Setup Required:**
```python
# Fixtures: matplotlib_pyplot, node_size, coords
```

## Step-by-Step Guide

### Step 1: "Tests for plot_markers and 'lyrz' display mode.\n\n    Tests that markers are plotted with the requested size\n    with display_mode='lyrz'. (See issue #3012 and PR #3013).\n    "

```python
"Tests for plot_markers and 'lyrz' display mode.\n\n    Tests that markers are plotted with the requested size\n    with display_mode='lyrz'. (See issue #3012 and PR #3013).\n    "
```

**Verification:**
```python
assert np.all(display_sizes == expected_sizes)
```

### Step 2: Assign display = plot_markers(...)

```python
display = plot_markers([1, 2, 3, 4], coords, display_mode='lyrz', node_size=node_size)
```

### Step 3: Assign display_sizes = unknown.get_sizes(...)

```python
display_sizes = axes.ax.collections[0].get_sizes()
```

**Verification:**
```python
assert np.all(display_sizes == expected_sizes)
```

### Step 4: Assign expected_sizes = value

```python
expected_sizes = node_size[-2:]
```

### Step 5: Assign expected_sizes = value

```python
expected_sizes = node_size[:-2]
```

### Step 6: Assign expected_sizes = node_size

```python
expected_sizes = node_size
```


## Complete Example

```python
# Setup
# Fixtures: matplotlib_pyplot, node_size, coords

# Workflow
"Tests for plot_markers and 'lyrz' display mode.\n\n    Tests that markers are plotted with the requested size\n    with display_mode='lyrz'. (See issue #3012 and PR #3013).\n    "
display = plot_markers([1, 2, 3, 4], coords, display_mode='lyrz', node_size=node_size)
for d, axes in display.axes.items():
    display_sizes = axes.ax.collections[0].get_sizes()
    if d == 'l':
        expected_sizes = node_size[-2:]
    elif d == 'r':
        expected_sizes = node_size[:-2]
    else:
        expected_sizes = node_size
    assert np.all(display_sizes == expected_sizes)
```

## Next Steps


---

*Source: test_plot_markers.py:50 | Complexity: Intermediate | Last updated: 2026-05-18*