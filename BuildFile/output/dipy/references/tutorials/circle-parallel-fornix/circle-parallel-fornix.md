# How To: Circle Parallel Fornix

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test circle parallel fornix

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

### Step 1: Assign circle = streamlines_in_circle(...)

```python
circle = streamlines_in_circle(100, step_size=2)
```

**Verification:**
```python
assert_equal(len(clusters), 1)
```

### Step 2: Assign parallel = streamlines_parallel(...)

```python
parallel = streamlines_parallel(100)
```

**Verification:**
```python
assert_equal(len(clusters), 3)
```

### Step 3: Assign thresholds = value

```python
thresholds = [1, 0.1]
```

**Verification:**
```python
assert_equal(len(clusters), 34)
```

### Step 4: Assign qbx_class = QuickBundlesX(...)

```python
qbx_class = QuickBundlesX(thresholds)
```

**Verification:**
```python
assert_equal(len(clusters), 1)
```

### Step 5: Assign tree = qbx_class.cluster(...)

```python
tree = qbx_class.cluster(circle)
```

**Verification:**
```python
assert_equal(len(clusters), 100)
```

### Step 6: Assign clusters = tree.get_clusters(...)

```python
clusters = tree.get_clusters(0)
```

### Step 7: Call assert_equal()

```python
assert_equal(len(clusters), 1)
```

### Step 8: Assign clusters = tree.get_clusters(...)

```python
clusters = tree.get_clusters(1)
```

### Step 9: Call assert_equal()

```python
assert_equal(len(clusters), 3)
```

### Step 10: Assign clusters = tree.get_clusters(...)

```python
clusters = tree.get_clusters(2)
```

### Step 11: Call assert_equal()

```python
assert_equal(len(clusters), 34)
```

### Step 12: Assign thresholds = value

```python
thresholds = [0.5]
```

### Step 13: Assign qbx_class = QuickBundlesX(...)

```python
qbx_class = QuickBundlesX(thresholds)
```

### Step 14: Assign tree = qbx_class.cluster(...)

```python
tree = qbx_class.cluster(parallel)
```

### Step 15: Assign clusters = tree.get_clusters(...)

```python
clusters = tree.get_clusters(0)
```

### Step 16: Call assert_equal()

```python
assert_equal(len(clusters), 1)
```

### Step 17: Assign clusters = tree.get_clusters(...)

```python
clusters = tree.get_clusters(1)
```

### Step 18: Call assert_equal()

```python
assert_equal(len(clusters), 100)
```


## Complete Example

```python
# Workflow
circle = streamlines_in_circle(100, step_size=2)
parallel = streamlines_parallel(100)
thresholds = [1, 0.1]
qbx_class = QuickBundlesX(thresholds)
tree = qbx_class.cluster(circle)
clusters = tree.get_clusters(0)
assert_equal(len(clusters), 1)
clusters = tree.get_clusters(1)
assert_equal(len(clusters), 3)
clusters = tree.get_clusters(2)
assert_equal(len(clusters), 34)
thresholds = [0.5]
qbx_class = QuickBundlesX(thresholds)
tree = qbx_class.cluster(parallel)
clusters = tree.get_clusters(0)
assert_equal(len(clusters), 1)
clusters = tree.get_clusters(1)
assert_equal(len(clusters), 100)
```

## Next Steps


---

*Source: test_qbx.py:171 | Complexity: Advanced | Last updated: 2026-05-18*