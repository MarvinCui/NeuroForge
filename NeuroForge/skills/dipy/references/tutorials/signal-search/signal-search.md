# How To: Signal Search

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test signal matching search.

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.reconst.force`


## Step-by-Step Guide

### Step 1: 'Test signal matching search.'

```python
'Test signal matching search.'
```

**Verification:**
```python
assert D.shape == (10, 20)
```

### Step 2: Assign signals = np.random.randn.astype(...)

```python
signals = np.random.randn(100, 50).astype(np.float32)
```

**Verification:**
```python
assert neighbors.shape == (10, 20)
```

### Step 3: Assign signals_norm = value

```python
signals_norm = signals / np.linalg.norm(signals, axis=1, keepdims=True)
```

### Step 4: Assign index = create_signal_index(...)

```python
index = create_signal_index(signals_norm)
```

### Step 5: Assign query = np.random.randn.astype(...)

```python
query = np.random.randn(10, 50).astype(np.float32)
```

### Step 6: Assign query_norm = value

```python
query_norm = query / np.linalg.norm(query, axis=1, keepdims=True)
```

### Step 7: Assign unknown = index.search(...)

```python
D, neighbors = index.search(query_norm, k=20)
```

**Verification:**
```python
assert D.shape == (10, 20)
```


## Complete Example

```python
# Workflow
'Test signal matching search.'
signals = np.random.randn(100, 50).astype(np.float32)
signals_norm = signals / np.linalg.norm(signals, axis=1, keepdims=True)
index = create_signal_index(signals_norm)
query = np.random.randn(10, 50).astype(np.float32)
query_norm = query / np.linalg.norm(query, axis=1, keepdims=True)
D, neighbors = index.search(query_norm, k=20)
assert D.shape == (10, 20)
assert neighbors.shape == (10, 20)
```

## Next Steps


---

*Source: test_force.py:97 | Complexity: Intermediate | Last updated: 2026-05-18*