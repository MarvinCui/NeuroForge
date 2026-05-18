# How To: Plot Connectome Edge Thresholding

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, mock, workflow, integration

## Overview

Workflow: Test for plot_connectome with edge thresholding.

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

### Step 1: 'Test for plot_connectome with edge thresholding.'

```python
'Test for plot_connectome with edge thresholding.'
```

**Verification:**
```python
assert len([patch for patch in ax.axes[direction].ax.patches if isinstance(patch, FancyArrow)]) == np.sum(np.abs(non_symmetric_matrix) >= thresh)
```

### Step 2: Assign thresh = 1.1

```python
thresh = 1.1
```

**Verification:**
```python
assert len([patch for patch in ax.axes[direction].ax.patches if isinstance(patch, FancyArrow)]) == np.sum(np.abs(non_symmetric_matrix) > np.percentile(np.abs(non_symmetric_matrix.ravel()), thresh))
```

### Step 3: Assign ax = plot_connectome(...)

```python
ax = plot_connectome(non_symmetric_matrix, node_coords, edge_threshold=thresh)
```

### Step 4: Assign thresh = 80

```python
thresh = 80
```

### Step 5: Assign ax = plot_connectome(...)

```python
ax = plot_connectome(non_symmetric_matrix, node_coords, edge_threshold=f'{thresh}%')
```

**Verification:**
```python
assert len([patch for patch in ax.axes[direction].ax.patches if isinstance(patch, FancyArrow)]) == np.sum(np.abs(non_symmetric_matrix) >= thresh)
```


## Complete Example

```python
# Setup
# Fixtures: node_coords, non_symmetric_matrix

# Workflow
'Test for plot_connectome with edge thresholding.'
thresh = 1.1
ax = plot_connectome(non_symmetric_matrix, node_coords, edge_threshold=thresh)
for direction in ['x', 'y', 'z']:
    assert len([patch for patch in ax.axes[direction].ax.patches if isinstance(patch, FancyArrow)]) == np.sum(np.abs(non_symmetric_matrix) >= thresh)
thresh = 80
ax = plot_connectome(non_symmetric_matrix, node_coords, edge_threshold=f'{thresh}%')
for direction in ['x', 'y', 'z']:
    assert len([patch for patch in ax.axes[direction].ax.patches if isinstance(patch, FancyArrow)]) == np.sum(np.abs(non_symmetric_matrix) > np.percentile(np.abs(non_symmetric_matrix.ravel()), thresh))
```

## Next Steps


---

*Source: test_plot_connectome.py:142 | Complexity: Intermediate | Last updated: 2026-05-18*