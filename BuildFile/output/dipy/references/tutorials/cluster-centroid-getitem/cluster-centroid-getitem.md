# How To: Cluster Centroid Getitem

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test cluster centroid getitem

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `copy`
- `itertools`
- `numpy`
- `numpy.testing`
- `dipy.segment.clustering`
- `dipy.testing`
- `dipy.testing.decorators`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign indices = list(...)

```python
indices = list(range(len(data)))
```

**Verification:**
```python
assert_equal(cluster[i], indices[i])
```

### Step 2: Call rng.shuffle()

```python
rng.shuffle(indices)
```

**Verification:**
```python
assert_array_equal(cluster[advanced_indices], [indices[i] for i in advanced_indices])
```

### Step 3: Assign advanced_indices = value

```python
advanced_indices = indices + [0, 1, 2, -1, -2, -3]
```

**Verification:**
```python
assert_raises(IndexError, cluster.__getitem__, len(cluster))
```

### Step 4: Assign centroid = np.zeros(...)

```python
centroid = np.zeros(features_shape)
```

**Verification:**
```python
assert_raises(IndexError, cluster.__getitem__, -len(cluster) - 1)
```

### Step 5: Assign cluster = ClusterCentroid(...)

```python
cluster = ClusterCentroid(centroid)
```

**Verification:**
```python
assert_equal(cluster[-1], indices[-1])
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(cluster[advanced_indices], [indices[i] for i in advanced_indices])
```

**Verification:**
```python
assert_array_equal(cluster[::2], indices[::2])
```

### Step 7: Call assert_raises()

```python
assert_raises(IndexError, cluster.__getitem__, len(cluster))
```

**Verification:**
```python
assert_arrays_equal(cluster[::-1], indices[::-1])
```

### Step 8: Call assert_raises()

```python
assert_raises(IndexError, cluster.__getitem__, -len(cluster) - 1)
```

**Verification:**
```python
assert_arrays_equal(cluster[:-1], indices[:-1])
```

### Step 9: Call assert_equal()

```python
assert_equal(cluster[-1], indices[-1])
```

**Verification:**
```python
assert_arrays_equal(cluster[1:], indices[1:])
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(cluster[::2], indices[::2])
```

**Verification:**
```python
assert_array_equal(cluster[i], data[indices[i]])
```

### Step 11: Call assert_arrays_equal()

```python
assert_arrays_equal(cluster[::-1], indices[::-1])
```

**Verification:**
```python
assert_arrays_equal(cluster[advanced_indices], [data[indices[i]] for i in advanced_indices])
```

### Step 12: Call assert_arrays_equal()

```python
assert_arrays_equal(cluster[:-1], indices[:-1])
```

**Verification:**
```python
assert_raises(IndexError, cluster.__getitem__, len(cluster))
```

### Step 13: Call assert_arrays_equal()

```python
assert_arrays_equal(cluster[1:], indices[1:])
```

**Verification:**
```python
assert_raises(IndexError, cluster.__getitem__, -len(cluster) - 1)
```

### Step 14: Assign cluster.refdata = data

```python
cluster.refdata = data
```

**Verification:**
```python
assert_array_equal(cluster[-1], data[indices[-1]])
```

### Step 15: Call assert_arrays_equal()

```python
assert_arrays_equal(cluster[advanced_indices], [data[indices[i]] for i in advanced_indices])
```

**Verification:**
```python
assert_arrays_equal(cluster[::2], [data[i] for i in indices[::2]])
```

### Step 16: Call assert_raises()

```python
assert_raises(IndexError, cluster.__getitem__, len(cluster))
```

**Verification:**
```python
assert_arrays_equal(cluster[::-1], [data[i] for i in indices[::-1]])
```

### Step 17: Call assert_raises()

```python
assert_raises(IndexError, cluster.__getitem__, -len(cluster) - 1)
```

**Verification:**
```python
assert_arrays_equal(cluster[:-1], [data[i] for i in indices[:-1]])
```

### Step 18: Call assert_array_equal()

```python
assert_array_equal(cluster[-1], data[indices[-1]])
```

**Verification:**
```python
assert_arrays_equal(cluster[1:], [data[i] for i in indices[1:]])
```

### Step 19: Call assert_arrays_equal()

```python
assert_arrays_equal(cluster[::2], [data[i] for i in indices[::2]])
```

### Step 20: Call assert_arrays_equal()

```python
assert_arrays_equal(cluster[::-1], [data[i] for i in indices[::-1]])
```

### Step 21: Call assert_arrays_equal()

```python
assert_arrays_equal(cluster[:-1], [data[i] for i in indices[:-1]])
```

### Step 22: Call assert_arrays_equal()

```python
assert_arrays_equal(cluster[1:], [data[i] for i in indices[1:]])
```

### Step 23: Call cluster.assign()

```python
cluster.assign(idx, (idx + 1) * features)
```

### Step 24: Call assert_equal()

```python
assert_equal(cluster[i], indices[i])
```

### Step 25: Call assert_array_equal()

```python
assert_array_equal(cluster[i], data[indices[i]])
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
indices = list(range(len(data)))
rng.shuffle(indices)
advanced_indices = indices + [0, 1, 2, -1, -2, -3]
centroid = np.zeros(features_shape)
cluster = ClusterCentroid(centroid)
for idx in indices:
    cluster.assign(idx, (idx + 1) * features)
for i in advanced_indices:
    assert_equal(cluster[i], indices[i])
assert_array_equal(cluster[advanced_indices], [indices[i] for i in advanced_indices])
assert_raises(IndexError, cluster.__getitem__, len(cluster))
assert_raises(IndexError, cluster.__getitem__, -len(cluster) - 1)
assert_equal(cluster[-1], indices[-1])
assert_array_equal(cluster[::2], indices[::2])
assert_arrays_equal(cluster[::-1], indices[::-1])
assert_arrays_equal(cluster[:-1], indices[:-1])
assert_arrays_equal(cluster[1:], indices[1:])
cluster.refdata = data
for i in advanced_indices:
    assert_array_equal(cluster[i], data[indices[i]])
assert_arrays_equal(cluster[advanced_indices], [data[indices[i]] for i in advanced_indices])
assert_raises(IndexError, cluster.__getitem__, len(cluster))
assert_raises(IndexError, cluster.__getitem__, -len(cluster) - 1)
assert_array_equal(cluster[-1], data[indices[-1]])
assert_arrays_equal(cluster[::2], [data[i] for i in indices[::2]])
assert_arrays_equal(cluster[::-1], [data[i] for i in indices[::-1]])
assert_arrays_equal(cluster[:-1], [data[i] for i in indices[:-1]])
assert_arrays_equal(cluster[1:], [data[i] for i in indices[1:]])
```

## Next Steps


---

*Source: test_clustering.py:221 | Complexity: Advanced | Last updated: 2026-05-18*