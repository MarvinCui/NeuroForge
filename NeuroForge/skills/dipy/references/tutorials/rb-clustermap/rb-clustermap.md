# How To: Rb Clustermap

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test rb clustermap

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `dipy.data`
- `dipy.io.streamline`
- `dipy.segment.bundles`
- `dipy.segment.clustering`
- `dipy.testing.decorators`
- `dipy.tracking.distances`
- `dipy.tracking.streamline`


## Step-by-Step Guide

### Step 1: Assign cluster_map = qbx_and_merge(...)

```python
cluster_map = qbx_and_merge(f, thresholds=[40, 25, 20, 10])
```

**Verification:**
```python
assert_equal(row.min(), 0)
```

### Step 2: Assign rb = RecoBundles(...)

```python
rb = RecoBundles(f, greater_than=0, less_than=1000000, cluster_map=cluster_map, clust_thr=10)
```

**Verification:**
```python
assert_equal(row.min(), 0)
```

### Step 3: Assign unknown = rb.recognize(...)

```python
rec_trans, rec_labels = rb.recognize(model_bundle=f2, model_clust_thr=5.0, reduction_thr=10)
```

### Step 4: Assign msg = 'Streamlines do not have the same number of points. *'

```python
msg = 'Streamlines do not have the same number of points. *'
```

### Step 5: Assign unknown = rb.refine(...)

```python
refine_trans, refine_labels = rb.refine(model_bundle=f2, pruned_streamlines=rec_trans, model_clust_thr=5.0, reduction_thr=10)
```

### Step 6: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=msg, category=UserWarning)
```

### Step 7: Assign D = bundles_distances_mam(...)

```python
D = bundles_distances_mam(f2, f[rec_labels])
```

### Step 8: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=msg, category=UserWarning)
```

### Step 9: Assign D = bundles_distances_mam(...)

```python
D = bundles_distances_mam(f2, f[refine_labels])
```

### Step 10: Call assert_equal()

```python
assert_equal(row.min(), 0)
```

### Step 11: Call assert_equal()

```python
assert_equal(row.min(), 0)
```


## Complete Example

```python
# Workflow
cluster_map = qbx_and_merge(f, thresholds=[40, 25, 20, 10])
rb = RecoBundles(f, greater_than=0, less_than=1000000, cluster_map=cluster_map, clust_thr=10)
rec_trans, rec_labels = rb.recognize(model_bundle=f2, model_clust_thr=5.0, reduction_thr=10)
msg = 'Streamlines do not have the same number of points. *'
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=msg, category=UserWarning)
    D = bundles_distances_mam(f2, f[rec_labels])
if len(f2) == len(rec_labels):
    for row in D:
        assert_equal(row.min(), 0)
refine_trans, refine_labels = rb.refine(model_bundle=f2, pruned_streamlines=rec_trans, model_clust_thr=5.0, reduction_thr=10)
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=msg, category=UserWarning)
    D = bundles_distances_mam(f2, f[refine_labels])
for row in D:
    assert_equal(row.min(), 0)
```

## Next Steps


---

*Source: test_bundles.py:166 | Complexity: Advanced | Last updated: 2026-05-18*