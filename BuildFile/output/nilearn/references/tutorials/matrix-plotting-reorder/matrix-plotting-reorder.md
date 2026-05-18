# How To: Matrix Plotting Reorder

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test matrix plotting reorder

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `itertools`
- `matplotlib`
- `matplotlib.pyplot`
- `numpy`
- `pandas`
- `pytest`
- `nilearn._utils.helpers`
- `nilearn.conftest`
- `nilearn.glm.first_level.design_matrix`
- `nilearn.glm.tests._testing`
- `nilearn.plotting.matrix._utils`
- `nilearn.plotting.matrix.matrix_plotting`

**Setup Required:**
```python
# Fixtures: matplotlib_pyplot, mat, labels
```

## Step-by-Step Guide

### Step 1: Assign idx = value

```python
idx = [2, 3, 5]
```

**Verification:**
```python
assert len(labels) == len(ax.axes.get_xticklabels())
```

### Step 2: Assign ax = plot_matrix(...)

```python
ax = plot_matrix(mat, labels=labels, reorder=True)
```

**Verification:**
```python
assert reordered_labels[:3] == idx or reordered_labels[-3:] == idx, 'Clustering does not find block structure.'
```

### Step 3: Assign reordered_labels = value

```python
reordered_labels = [int(lbl.get_text()) for lbl in ax.axes.get_xticklabels()]
```

**Verification:**
```python
assert reordered_labels[:3] == idx or reordered_labels[-3:] == idx, 'Clustering does not find block structure.'
```

### Step 4: Assign ax = plot_matrix(...)

```python
ax = plot_matrix(mat, labels=labels, reorder='complete')
```

### Step 5: Assign unknown = 1

```python
mat[perm] = 1
```


## Complete Example

```python
# Setup
# Fixtures: matplotlib_pyplot, mat, labels

# Workflow
idx = [2, 3, 5]
for perm in permutations(idx, 2):
    mat[perm] = 1
ax = plot_matrix(mat, labels=labels, reorder=True)
assert len(labels) == len(ax.axes.get_xticklabels())
reordered_labels = [int(lbl.get_text()) for lbl in ax.axes.get_xticklabels()]
assert reordered_labels[:3] == idx or reordered_labels[-3:] == idx, 'Clustering does not find block structure.'
ax = plot_matrix(mat, labels=labels, reorder='complete')
```

## Next Steps


---

*Source: test_matrix_plotting.py:114 | Complexity: Intermediate | Last updated: 2026-05-18*