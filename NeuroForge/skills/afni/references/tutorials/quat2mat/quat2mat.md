# How To: Quat2Mat

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test quat2mat

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy`
- `nose.tools`
- `numpy.testing`
- `numpy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign M = nq.quat2mat(...)

```python
M = nq.quat2mat([1, 0, 0, 0])
```

### Step 2: yield (assert_array_almost_equal, M, np.eye(3))

```python
yield (assert_array_almost_equal, M, np.eye(3))
```

### Step 3: Assign M = nq.quat2mat(...)

```python
M = nq.quat2mat([3, 0, 0, 0])
```

### Step 4: yield (assert_array_almost_equal, M, np.eye(3))

```python
yield (assert_array_almost_equal, M, np.eye(3))
```

### Step 5: Assign M = nq.quat2mat(...)

```python
M = nq.quat2mat([0, 1, 0, 0])
```

### Step 6: yield (assert_array_almost_equal, M, np.diag([1, -1, -1]))

```python
yield (assert_array_almost_equal, M, np.diag([1, -1, -1]))
```

### Step 7: Assign M = nq.quat2mat(...)

```python
M = nq.quat2mat([0, 2, 0, 0])
```

### Step 8: yield (assert_array_almost_equal, M, np.diag([1, -1, -1]))

```python
yield (assert_array_almost_equal, M, np.diag([1, -1, -1]))
```

### Step 9: Assign M = nq.quat2mat(...)

```python
M = nq.quat2mat([0, 0, 0, 0])
```

### Step 10: yield (assert_array_almost_equal, M, np.eye(3))

```python
yield (assert_array_almost_equal, M, np.eye(3))
```


## Complete Example

```python
# Workflow
M = nq.quat2mat([1, 0, 0, 0])
yield (assert_array_almost_equal, M, np.eye(3))
M = nq.quat2mat([3, 0, 0, 0])
yield (assert_array_almost_equal, M, np.eye(3))
M = nq.quat2mat([0, 1, 0, 0])
yield (assert_array_almost_equal, M, np.diag([1, -1, -1]))
M = nq.quat2mat([0, 2, 0, 0])
yield (assert_array_almost_equal, M, np.diag([1, -1, -1]))
M = nq.quat2mat([0, 0, 0, 0])
yield (assert_array_almost_equal, M, np.eye(3))
```

## Next Steps


---

*Source: test_quaternions.py:87 | Complexity: Advanced | Last updated: 2026-05-18*