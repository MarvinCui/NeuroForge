# How To: Quickbundles 2D

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test quickbundles 2D

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `itertools`
- `numpy`
- `numpy.testing`
- `dipy.segment.clustering`
- `dipy.segment.clustering_algorithms`
- `dipy.segment.featurespeed`
- `dipy.segment.metricspeed`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.testing.memory`
- `dipy.tracking.streamline`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign data = value

```python
data = []
```

**Verification:**
```python
assert_equal(sorted(cluster.indices), sorted(cluster_truth))
```

### Step 2: Assign data = np.array(...)

```python
data = np.array(data, dtype=dtype)
```

**Verification:**
```python
assert_equal(len(subclusters), len(cluster))
```

### Step 3: Assign clusters_truth = value

```python
clusters_truth = [[0], [1, 2], [3, 4, 5], [6, 7, 8, 9], [10, 11, 12, 13, 14]]
```

**Verification:**
```python
assert_equal(sorted(itertools.chain(*subclusters)), sorted(cluster.indices))
```

### Step 4: Assign threshold = value

```python
threshold = np.sqrt(2 * 10 ** 2) - np.sqrt(2)
```

**Verification:**
```python
assert_equal(len(clusters), 1)
```

### Step 5: Assign metric = dipysmetric.SumPointwiseEuclideanMetric(...)

```python
metric = dipysmetric.SumPointwiseEuclideanMetric()
```

**Verification:**
```python
assert_equal(len(clusters[0]), len(data))
```

### Step 6: Assign ordering = np.arange(...)

```python
ordering = np.arange(len(data))
```

**Verification:**
```python
assert_array_equal(clusters[0].indices, range(len(data)))
```

### Step 7: Assign clusters = quickbundles(...)

```python
clusters = quickbundles(data, metric, threshold=np.inf)
```

**Verification:**
```python
assert_equal(len(clusters), len(data))
```

### Step 8: Call assert_equal()

```python
assert_equal(len(clusters), 1)
```

**Verification:**
```python
assert_array_equal(list(map(len, clusters)), np.ones(len(data)))
```

### Step 9: Call assert_equal()

```python
assert_equal(len(clusters[0]), len(data))
```

**Verification:**
```python
assert_array_equal([idx for cluster in clusters for idx in cluster.indices], range(len(data)))
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(clusters[0].indices, range(len(data)))
```

### Step 11: Assign clusters = quickbundles(...)

```python
clusters = quickbundles(data, metric, threshold=0)
```

### Step 12: Call assert_equal()

```python
assert_equal(len(clusters), len(data))
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(list(map(len, clusters)), np.ones(len(data)))
```

### Step 14: Call assert_array_equal()

```python
assert_array_equal([idx for cluster in clusters for idx in cluster.indices], range(len(data)))
```

### Step 15: Call rng.shuffle()

```python
rng.shuffle(ordering)
```

### Step 16: Assign clusters = quickbundles(...)

```python
clusters = quickbundles(data, metric, threshold, ordering=ordering)
```

### Step 17: Assign subclusters = quickbundles(...)

```python
subclusters = quickbundles(data, metric, threshold=0, ordering=cluster.indices)
```

### Step 18: Call assert_equal()

```python
assert_equal(len(subclusters), len(cluster))
```

### Step 19: Call assert_equal()

```python
assert_equal(sorted(itertools.chain(*subclusters)), sorted(cluster.indices))
```

### Step 20: Call assert_equal()

```python
assert_equal(sorted(cluster.indices), sorted(cluster_truth))
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
data = []
data += [rng.standard_normal((1, 2)) + np.array([0, 0]) for _ in range(1)]
data += [rng.standard_normal((1, 2)) + np.array([10, 10]) for _ in range(2)]
data += [rng.standard_normal((1, 2)) + np.array([-10, 10]) for _ in range(3)]
data += [rng.standard_normal((1, 2)) + np.array([10, -10]) for _ in range(4)]
data += [rng.standard_normal((1, 2)) + np.array([-10, -10]) for _ in range(5)]
data = np.array(data, dtype=dtype)
clusters_truth = [[0], [1, 2], [3, 4, 5], [6, 7, 8, 9], [10, 11, 12, 13, 14]]
threshold = np.sqrt(2 * 10 ** 2) - np.sqrt(2)
metric = dipysmetric.SumPointwiseEuclideanMetric()
ordering = np.arange(len(data))
for _ in range(100):
    rng.shuffle(ordering)
    clusters = quickbundles(data, metric, threshold, ordering=ordering)
    for cluster in clusters:
        for cluster_truth in clusters_truth:
            if cluster_truth[0] in cluster.indices:
                assert_equal(sorted(cluster.indices), sorted(cluster_truth))
for cluster in clusters:
    subclusters = quickbundles(data, metric, threshold=0, ordering=cluster.indices)
    assert_equal(len(subclusters), len(cluster))
    assert_equal(sorted(itertools.chain(*subclusters)), sorted(cluster.indices))
clusters = quickbundles(data, metric, threshold=np.inf)
assert_equal(len(clusters), 1)
assert_equal(len(clusters[0]), len(data))
assert_array_equal(clusters[0].indices, range(len(data)))
clusters = quickbundles(data, metric, threshold=0)
assert_equal(len(clusters), len(data))
assert_array_equal(list(map(len, clusters)), np.ones(len(data)))
assert_array_equal([idx for cluster in clusters for idx in cluster.indices], range(len(data)))
```

## Next Steps


---

*Source: test_quickbundles.py:68 | Complexity: Advanced | Last updated: 2026-05-18*