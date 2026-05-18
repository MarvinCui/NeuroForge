# How To: Hierarchical K Means

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test hierarchical k means

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.data_gen`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.helpers`
- `nilearn._utils.versions`
- `nilearn.maskers`
- `nilearn.regions.hierarchical_kmeans_clustering`
- `nilearn.surface`
- `nilearn.surface.tests.test_surface`


## Step-by-Step Guide

### Step 1: Assign X = value

```python
X = [[10, -10, 30], [12, -8, 24]]
```

**Verification:**
```python
assert_array_almost_equal(test_labels, truth_labels)
```

### Step 2: Assign truth_labels = np.tile(...)

```python
truth_labels = np.tile([0, 1, 2], 5)
```

### Step 3: Assign X = value

```python
X = np.tile(X, 5).T
```

### Step 4: Assign test_labels = hierarchical_k_means(...)

```python
test_labels = hierarchical_k_means(X, 3)
```

### Step 5: Assign truth_labels = np.tile(...)

```python
truth_labels = np.tile([test_labels[0], test_labels[1], test_labels[2]], 5)
```

### Step 6: Call assert_array_almost_equal()

```python
assert_array_almost_equal(test_labels, truth_labels)
```


## Complete Example

```python
# Workflow
X = [[10, -10, 30], [12, -8, 24]]
truth_labels = np.tile([0, 1, 2], 5)
X = np.tile(X, 5).T
test_labels = hierarchical_k_means(X, 3)
truth_labels = np.tile([test_labels[0], test_labels[1], test_labels[2]], 5)
assert_array_almost_equal(test_labels, truth_labels)
```

## Next Steps


---

*Source: test_hierarchical_kmeans_clustering.py:96 | Complexity: Intermediate | Last updated: 2026-05-18*