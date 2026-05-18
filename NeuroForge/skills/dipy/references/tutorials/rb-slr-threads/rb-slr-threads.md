# How To: Rb Slr Threads

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test rb slr threads

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign rb_multi = RecoBundles(...)

```python
rb_multi = RecoBundles(f, greater_than=0, clust_thr=10, rng=rng)
```

**Verification:**
```python
assert_almost_equal(row.min(), 0, decimal=4)
```

### Step 2: Assign unknown = rb_multi.recognize(...)

```python
rec_trans_multi_threads, _ = rb_multi.recognize(model_bundle=f2, model_clust_thr=5.0, reduction_thr=10, slr=True, num_threads=None)
```

### Step 3: Assign rb_single = RecoBundles(...)

```python
rb_single = RecoBundles(f, greater_than=0, clust_thr=10, rng=np.random.default_rng(42))
```

### Step 4: Assign unknown = rb_single.recognize(...)

```python
rec_trans_single_thread, _ = rb_single.recognize(model_bundle=f2, model_clust_thr=5.0, reduction_thr=10, slr=True, num_threads=1)
```

### Step 5: Assign msg = 'Streamlines do not have the same number of points. *'

```python
msg = 'Streamlines do not have the same number of points. *'
```

### Step 6: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', message=msg, category=UserWarning)
```

### Step 7: Assign D = bundles_distances_mam(...)

```python
D = bundles_distances_mam(rec_trans_multi_threads, rec_trans_single_thread)
```

### Step 8: Call assert_almost_equal()

```python
assert_almost_equal(row.min(), 0, decimal=4)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
rb_multi = RecoBundles(f, greater_than=0, clust_thr=10, rng=rng)
rec_trans_multi_threads, _ = rb_multi.recognize(model_bundle=f2, model_clust_thr=5.0, reduction_thr=10, slr=True, num_threads=None)
rb_single = RecoBundles(f, greater_than=0, clust_thr=10, rng=np.random.default_rng(42))
rec_trans_single_thread, _ = rb_single.recognize(model_bundle=f2, model_clust_thr=5.0, reduction_thr=10, slr=True, num_threads=1)
msg = 'Streamlines do not have the same number of points. *'
with warnings.catch_warnings():
    warnings.filterwarnings('ignore', message=msg, category=UserWarning)
    D = bundles_distances_mam(rec_trans_multi_threads, rec_trans_single_thread)
for row in D:
    assert_almost_equal(row.min(), 0, decimal=4)
```

## Next Steps


---

*Source: test_bundles.py:101 | Complexity: Advanced | Last updated: 2026-05-18*