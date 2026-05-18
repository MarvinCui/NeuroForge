# How To: Adjacency Equiv

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test adjacency equivalence for lattice adjacency.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne.stats`
- `sklearn.feature_extraction`

**Setup Required:**
```python
# Fixtures: shape
```

## Step-by-Step Guide

### Step 1: 'Test adjacency equivalence for lattice adjacency.'

```python
'Test adjacency equivalence for lattice adjacency.'
```

**Verification:**
```python
assert conn.shape == conn_sk.shape == want_shape
```

### Step 2: Assign sk_shape = value

```python
sk_shape = shape if len(shape) > 1 else shape + (1,)
```

**Verification:**
```python
assert (conn.data == 1.0).all()
```

### Step 3: Assign conn_sk = grid_to_graph.toarray(...)

```python
conn_sk = grid_to_graph(*sk_shape).toarray()
```

**Verification:**
```python
assert np.isin(conn, [0, 1, 2, 3]).all()
```

### Step 4: Assign conn = combine_adjacency(...)

```python
conn = combine_adjacency(*shape)
```

**Verification:**
```python
assert conn.shape == conn_sk.shape
```

### Step 5: Assign want_shape = value

```python
want_shape = (np.prod(shape),) * 2
```

**Verification:**
```python
assert_array_equal(conn, conn_sk)
```

### Step 6: Assign conn = conn.toarray(...)

```python
conn = conn.toarray()
```

**Verification:**
```python
assert np.isin(conn, [0, 1, 2, 3]).all()
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(conn, conn_sk)
```


## Complete Example

```python
# Setup
# Fixtures: shape

# Workflow
'Test adjacency equivalence for lattice adjacency.'
from sklearn.feature_extraction import grid_to_graph
sk_shape = shape if len(shape) > 1 else shape + (1,)
conn_sk = grid_to_graph(*sk_shape).toarray()
conn = combine_adjacency(*shape)
want_shape = (np.prod(shape),) * 2
assert conn.shape == conn_sk.shape == want_shape
assert (conn.data == 1.0).all()
conn = conn.toarray()
assert np.isin(conn, [0, 1, 2, 3]).all()
assert conn.shape == conn_sk.shape
assert_array_equal(conn, conn_sk)
```

## Next Steps


---

*Source: test_adjacency.py:28 | Complexity: Intermediate | Last updated: 2026-05-18*