# How To: With Simulated Bundles

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test with simulated bundles

## Prerequisites

**Required Modules:**
- `itertools`
- `numpy`
- `numpy.testing`
- `dipy.segment.clustering`
- `dipy.segment.featurespeed`
- `dipy.segment.metricspeed`
- `dipy.testing.decorators`
- `dipy.tracking.streamline`


## Step-by-Step Guide

### Step 1: Assign streamlines = simulated_bundle(...)

```python
streamlines = simulated_bundle(3, False, 2)
```

**Verification:**
```python
assert_equal(tree.leaves[0].indices[0], 0)
```

### Step 2: Assign thresholds = value

```python
thresholds = [10, 3, 1]
```

**Verification:**
```python
assert_equal(tree.leaves[2][0], 2)
```

### Step 3: Assign qbx_class = QuickBundlesX(...)

```python
qbx_class = QuickBundlesX(thresholds)
```

**Verification:**
```python
assert_array_equal(clusters[0][0], np.array([[0.0, -10.0, -5.0], [0.0, 10.0, -5.0]]))
```

### Step 4: Assign tree = qbx_class.cluster(...)

```python
tree = qbx_class.cluster(streamlines)
```

### Step 5: Call assert_equal()

```python
assert_equal(tree.leaves[0].indices[0], 0)
```

### Step 6: Call assert_equal()

```python
assert_equal(tree.leaves[2][0], 2)
```

### Step 7: Assign clusters.refdata = streamlines

```python
clusters.refdata = streamlines
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(clusters[0][0], np.array([[0.0, -10.0, -5.0], [0.0, 10.0, -5.0]]))
```

### Step 9: Assign clusters = tree.get_clusters(...)

```python
clusters = tree.get_clusters(level)
```


## Complete Example

```python
# Workflow
streamlines = simulated_bundle(3, False, 2)
thresholds = [10, 3, 1]
qbx_class = QuickBundlesX(thresholds)
tree = qbx_class.cluster(streamlines)
for level in range(len(thresholds) + 1):
    clusters = tree.get_clusters(level)
assert_equal(tree.leaves[0].indices[0], 0)
assert_equal(tree.leaves[2][0], 2)
clusters.refdata = streamlines
assert_array_equal(clusters[0][0], np.array([[0.0, -10.0, -5.0], [0.0, 10.0, -5.0]]))
```

## Next Steps


---

*Source: test_qbx.py:141 | Complexity: Advanced | Last updated: 2026-05-18*