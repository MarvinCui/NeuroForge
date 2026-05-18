# How To: Inverse

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test inverse

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy`
- `nose.tools`
- `numpy.testing`
- `numpy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign iq = nq.inverse(...)

```python
iq = nq.inverse((1, 0, 0, 0))
```

### Step 2: yield (assert_true, iq.dtype.kind == 'f')

```python
yield (assert_true, iq.dtype.kind == 'f')
```

### Step 3: Assign iq = nq.inverse(...)

```python
iq = nq.inverse(q)
```

### Step 4: Assign iqM = nq.quat2mat(...)

```python
iqM = nq.quat2mat(iq)
```

### Step 5: Assign iM = np.linalg.inv(...)

```python
iM = np.linalg.inv(M)
```

### Step 6: yield (assert_true, np.allclose(iM, iqM))

```python
yield (assert_true, np.allclose(iM, iqM))
```


## Complete Example

```python
# Workflow
iq = nq.inverse((1, 0, 0, 0))
yield (assert_true, iq.dtype.kind == 'f')
for M, q in eg_pairs:
    iq = nq.inverse(q)
    iqM = nq.quat2mat(iq)
    iM = np.linalg.inv(M)
    yield (assert_true, np.allclose(iM, iqM))
```

## Next Steps


---

*Source: test_quaternions.py:101 | Complexity: Intermediate | Last updated: 2026-05-18*