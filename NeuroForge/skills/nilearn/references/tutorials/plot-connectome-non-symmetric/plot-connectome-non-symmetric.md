# How To: Plot Connectome Non Symmetric

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, mock, workflow, integration

## Overview

Workflow: Tests for plot_connectome with non symmetric adjacency matrices.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `matplotlib.patches`
- `scipy`
- `nilearn.plotting`

**Setup Required:**
```python
# Fixtures: node_coords, non_symmetric_matrix
```

## Step-by-Step Guide

### Step 1: 'Tests for plot_connectome with non symmetric adjacency matrices.'

```python
'Tests for plot_connectome with non symmetric adjacency matrices.'
```

**Verification:**
```python
assert len([patch for patch in ax.axes[direction].ax.patches if isinstance(patch, FancyArrow)]) == np.prod(non_symmetric_matrix.shape)
```

### Step 2: Assign ax = plot_connectome(...)

```python
ax = plot_connectome(non_symmetric_matrix, node_coords, display_mode='ortho')
```

**Verification:**
```python
assert not [patch for patch in ax.axes['l'].ax.patches if isinstance(patch, FancyArrow)]
```

### Step 3: Assign unknown = 0.0

```python
non_symmetric_matrix[1, 0] = 0.0
```

**Verification:**
```python
assert len([patch for patch in ax.axes[direction].ax.patches if isinstance(patch, FancyArrow)]) == np.prod(non_symmetric_matrix.shape) - 2
```

### Step 4: Assign unknown = 0.0

```python
non_symmetric_matrix[2, 3] = 0.0
```

### Step 5: Assign ax = plot_connectome(...)

```python
ax = plot_connectome(non_symmetric_matrix, node_coords, display_mode='lzry')
```

**Verification:**
```python
assert not [patch for patch in ax.axes['l'].ax.patches if isinstance(patch, FancyArrow)]
```


## Complete Example

```python
# Setup
# Fixtures: node_coords, non_symmetric_matrix

# Workflow
'Tests for plot_connectome with non symmetric adjacency matrices.'
ax = plot_connectome(non_symmetric_matrix, node_coords, display_mode='ortho')
for direction in ['x', 'y', 'z']:
    assert len([patch for patch in ax.axes[direction].ax.patches if isinstance(patch, FancyArrow)]) == np.prod(non_symmetric_matrix.shape)
non_symmetric_matrix[1, 0] = 0.0
non_symmetric_matrix[2, 3] = 0.0
ax = plot_connectome(non_symmetric_matrix, node_coords, display_mode='lzry')
assert not [patch for patch in ax.axes['l'].ax.patches if isinstance(patch, FancyArrow)]
for direction in ['z', 'r', 'y']:
    assert len([patch for patch in ax.axes[direction].ax.patches if isinstance(patch, FancyArrow)]) == np.prod(non_symmetric_matrix.shape) - 2
```

## Next Steps


---

*Source: test_plot_connectome.py:99 | Complexity: Intermediate | Last updated: 2026-05-18*