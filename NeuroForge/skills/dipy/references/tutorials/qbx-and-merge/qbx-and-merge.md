# How To: Qbx And Merge

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test qbx and merge

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `itertools`
- `numpy`
- `numpy.testing`
- `dipy.segment.clustering`
- `dipy.segment.featurespeed`
- `dipy.segment.metricspeed`
- `dipy.testing.decorators`
- `dipy.tracking.streamline`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign bundles = bearing_bundles(...)

```python
bundles = bearing_bundles(4, 2)
```

**Verification:**
```python
assert_equal(len(qbx_centroids) > len(qbxm_centroids), True)
```

### Step 2: Call bundles.append()

```python
bundles.append(straight_bundle(1, rng=rng))
```

**Verification:**
```python
assert_array_equal(qbxm_clusters[0][0], streamlines[streamline_idx])
```

### Step 3: Assign streamlines = Streamlines(...)

```python
streamlines = Streamlines(list(itertools.chain(*bundles)))
```

### Step 4: Assign thresholds = value

```python
thresholds = [10, 2, 1]
```

### Step 5: Assign qbxm = qbx_and_merge(...)

```python
qbxm = qbx_and_merge(streamlines, thresholds, rng=rng)
```

### Step 6: Assign qbxm_centroids = value

```python
qbxm_centroids = qbxm.centroids
```

### Step 7: Assign qbxm_clusters = value

```python
qbxm_clusters = qbxm.clusters
```

### Step 8: Assign qbx = QuickBundlesX(...)

```python
qbx = QuickBundlesX(thresholds)
```

### Step 9: Assign tree = qbx.cluster(...)

```python
tree = qbx.cluster(streamlines)
```

### Step 10: Assign qbx_centroids = value

```python
qbx_centroids = tree.get_clusters(3).centroids
```

### Step 11: Call assert_equal()

```python
assert_equal(len(qbx_centroids) > len(qbxm_centroids), True)
```

### Step 12: Assign streamline_idx = value

```python
streamline_idx = qbxm_clusters[0].indices[0]
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(qbxm_clusters[0][0], streamlines[streamline_idx])
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
bundles = bearing_bundles(4, 2)
bundles.append(straight_bundle(1, rng=rng))
streamlines = Streamlines(list(itertools.chain(*bundles)))
thresholds = [10, 2, 1]
qbxm = qbx_and_merge(streamlines, thresholds, rng=rng)
qbxm_centroids = qbxm.centroids
qbxm_clusters = qbxm.clusters
qbx = QuickBundlesX(thresholds)
tree = qbx.cluster(streamlines)
qbx_centroids = tree.get_clusters(3).centroids
assert_equal(len(qbx_centroids) > len(qbxm_centroids), True)
streamline_idx = qbxm_clusters[0].indices[0]
assert_array_equal(qbxm_clusters[0][0], streamlines[streamline_idx])
```

## Next Steps


---

*Source: test_qbx.py:212 | Complexity: Advanced | Last updated: 2026-05-18*