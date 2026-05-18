# How To: Rb No Neighb

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test rb no neighb

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

### Step 1: Assign b = Streamlines(...)

```python
b = Streamlines(fornix)
```

**Verification:**
```python
assert_equal(len(refine_labels), 0)
```

### Step 2: Assign b1 = b.copy(...)

```python
b1 = b.copy()
```

**Verification:**
```python
assert_equal(len(refine_trans), 0)
```

### Step 3: Assign b2 = unknown.copy(...)

```python
b2 = b1[:20].copy()
```

**Verification:**
```python
assert_equal(len(rec_labels), 0)
```

### Step 4: Assign b3 = unknown.copy(...)

```python
b3 = b1[:20].copy()
```

**Verification:**
```python
assert_equal(len(rec_trans), 0)
```

### Step 5: Call b.extend()

```python
b.extend(b3)
```

### Step 6: Assign rb = RecoBundles(...)

```python
rb = RecoBundles(b, greater_than=0, clust_thr=10)
```

### Step 7: Assign unknown = rb.recognize(...)

```python
rec_trans, rec_labels = rb.recognize(model_bundle=b2, model_clust_thr=5.0, reduction_thr=10)
```

### Step 8: Assign unknown = rb.refine(...)

```python
refine_trans, refine_labels = rb.refine(model_bundle=b2, pruned_streamlines=rec_trans, model_clust_thr=5.0, reduction_thr=10)
```

### Step 9: Call assert_equal()

```python
assert_equal(len(refine_labels), 0)
```

### Step 10: Call assert_equal()

```python
assert_equal(len(refine_trans), 0)
```

### Step 11: Call assert_equal()

```python
assert_equal(len(rec_labels), 0)
```

### Step 12: Call assert_equal()

```python
assert_equal(len(rec_trans), 0)
```


## Complete Example

```python
# Workflow
b = Streamlines(fornix)
b1 = b.copy()
b2 = b1[:20].copy()
b2._data += np.array([100, 0, 0])
b3 = b1[:20].copy()
b3._data += np.array([300, 0, 0])
b.extend(b3)
rb = RecoBundles(b, greater_than=0, clust_thr=10)
rec_trans, rec_labels = rb.recognize(model_bundle=b2, model_clust_thr=5.0, reduction_thr=10)
if len(rec_trans) > 0:
    refine_trans, refine_labels = rb.refine(model_bundle=b2, pruned_streamlines=rec_trans, model_clust_thr=5.0, reduction_thr=10)
    assert_equal(len(refine_labels), 0)
    assert_equal(len(refine_trans), 0)
else:
    assert_equal(len(rec_labels), 0)
    assert_equal(len(rec_trans), 0)
```

## Next Steps


---

*Source: test_bundles.py:202 | Complexity: Advanced | Last updated: 2026-05-18*