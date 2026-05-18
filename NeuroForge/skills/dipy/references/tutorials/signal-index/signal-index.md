# How To: Signal Index

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test SignalIndex inner product search.

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.reconst.force`


## Step-by-Step Guide

### Step 1: 'Test SignalIndex inner product search.'

```python
'Test SignalIndex inner product search.'
```

**Verification:**
```python
assert index.ntotal == 100
```

### Step 2: Assign index = SignalIndex(...)

```python
index = SignalIndex(10)
```

**Verification:**
```python
assert D.shape == (5, 10)
```

### Step 3: Assign vectors = np.random.randn.astype(...)

```python
vectors = np.random.randn(100, 10).astype(np.float32)
```

**Verification:**
```python
assert neighbors.shape == (5, 10)
```

### Step 4: Call index.add()

```python
index.add(vectors)
```

**Verification:**
```python
assert np.all(D[i, :-1] >= D[i, 1:])
```

### Step 5: Assign query = np.random.randn.astype(...)

```python
query = np.random.randn(5, 10).astype(np.float32)
```

### Step 6: Assign unknown = index.search(...)

```python
D, neighbors = index.search(query, k=10)
```

**Verification:**
```python
assert D.shape == (5, 10)
```


## Complete Example

```python
# Workflow
'Test SignalIndex inner product search.'
index = SignalIndex(10)
vectors = np.random.randn(100, 10).astype(np.float32)
index.add(vectors)
assert index.ntotal == 100
query = np.random.randn(5, 10).astype(np.float32)
D, neighbors = index.search(query, k=10)
assert D.shape == (5, 10)
assert neighbors.shape == (5, 10)
for i in range(5):
    assert np.all(D[i, :-1] >= D[i, 1:])
```

## Next Steps


---

*Source: test_force.py:64 | Complexity: Intermediate | Last updated: 2026-05-18*