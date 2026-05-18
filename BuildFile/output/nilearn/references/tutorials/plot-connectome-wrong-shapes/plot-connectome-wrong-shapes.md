# How To: Plot Connectome Wrong Shapes

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Tests that ValueErrors are raised when wrong shapes for node_coords        or adjacency_matrix are given.
    

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `matplotlib.patches`
- `scipy`
- `nilearn.plotting`


## Step-by-Step Guide

### Step 1: 'Tests that ValueErrors are raised when wrong shapes for node_coords        or adjacency_matrix are given.\n    '

```python
'Tests that ValueErrors are raised when wrong shapes for node_coords        or adjacency_matrix are given.\n    '
```

### Step 2: Assign kwargs = value

```python
kwargs = {'display_mode': 'x'}
```

### Step 3: Assign node_coords = np.arange.reshape(...)

```python
node_coords = np.arange(2 * 3).reshape((2, 3))
```

### Step 4: Assign adjacency_matrix = np.array(...)

```python
adjacency_matrix = np.array([[1.0, 2.0], [2.0, 1.0]])
```

### Step 5: Assign wrong_adjacency_matrix = np.zeros(...)

```python
wrong_adjacency_matrix = np.zeros((3, 3))
```

### Step 6: Call plot_connectome()

```python
plot_connectome(adjacency_matrix[:1, :], node_coords, **kwargs)
```

### Step 7: Call plot_connectome()

```python
plot_connectome(adjacency_matrix, node_coords[:, 2], **kwargs)
```

### Step 8: Call plot_connectome()

```python
plot_connectome(wrong_adjacency_matrix, node_coords, **kwargs)
```


## Complete Example

```python
# Workflow
'Tests that ValueErrors are raised when wrong shapes for node_coords        or adjacency_matrix are given.\n    '
kwargs = {'display_mode': 'x'}
node_coords = np.arange(2 * 3).reshape((2, 3))
adjacency_matrix = np.array([[1.0, 2.0], [2.0, 1.0]])
with pytest.raises(ValueError, match='supposed to have shape \\(n, n\\).+\\(1L?, 2L?\\)'):
    plot_connectome(adjacency_matrix[:1, :], node_coords, **kwargs)
with pytest.raises(ValueError, match='shape \\(2L?, 3L?\\).+\\(2L?,\\)'):
    plot_connectome(adjacency_matrix, node_coords[:, 2], **kwargs)
wrong_adjacency_matrix = np.zeros((3, 3))
with pytest.raises(ValueError, match='Shape mismatch.+\\(3L?, 3L?\\).+\\(2L?, 3L?\\)'):
    plot_connectome(wrong_adjacency_matrix, node_coords, **kwargs)
```

## Next Steps


---

*Source: test_plot_connectome.py:249 | Complexity: Advanced | Last updated: 2026-05-18*