# How To: Argmax From Countarrs

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test argmax from countarrs

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.reconst.recspeed`


## Step-by-Step Guide

### Step 1: Assign vals = np.arange(...)

```python
vals = np.arange(10, dtype=float)
```

### Step 2: Assign vertinds = np.arange(...)

```python
vertinds = np.arange(10, dtype=np.uint32)
```

### Step 3: Assign adj_counts = np.ones(...)

```python
adj_counts = np.ones((10,), dtype=np.uint32)
```

### Step 4: Assign adj_inds_raw = value

```python
adj_inds_raw = np.arange(10, dtype=np.uint32)[::-1]
```

### Step 5: Assign adj_inds = adj_inds_raw.copy(...)

```python
adj_inds = adj_inds_raw.copy()
```

### Step 6: Call argmax_from_countarrs()

```python
argmax_from_countarrs(vals, vertinds, adj_counts, adj_inds)
```

### Step 7: Call argmax_from_countarrs()

```python
argmax_from_countarrs(vals, vertinds, adj_counts, adj_inds_raw)
```

### Step 8: Call argmax_from_countarrs()

```python
argmax_from_countarrs(vals, vertinds[:-1], adj_counts, adj_inds)
```

### Step 9: Call argmax_from_countarrs()

```python
argmax_from_countarrs(vals, vertinds, adj_counts, adj_inds[:-1])
```

### Step 10: Call argmax_from_countarrs()

```python
argmax_from_countarrs(vals[:-1], vertinds, adj_counts, adj_inds)
```


## Complete Example

```python
# Workflow
vals = np.arange(10, dtype=float)
vertinds = np.arange(10, dtype=np.uint32)
adj_counts = np.ones((10,), dtype=np.uint32)
adj_inds_raw = np.arange(10, dtype=np.uint32)[::-1]
adj_inds = adj_inds_raw.copy()
argmax_from_countarrs(vals, vertinds, adj_counts, adj_inds)
with assert_raises(ValueError):
    argmax_from_countarrs(vals, vertinds, adj_counts, adj_inds_raw)
with assert_raises(ValueError):
    argmax_from_countarrs(vals, vertinds[:-1], adj_counts, adj_inds)
with assert_raises(IndexError):
    argmax_from_countarrs(vals, vertinds, adj_counts, adj_inds[:-1])
with assert_raises(IndexError):
    argmax_from_countarrs(vals[:-1], vertinds, adj_counts, adj_inds)
```

## Next Steps


---

*Source: test_reco_utils.py:18 | Complexity: Advanced | Last updated: 2026-05-18*