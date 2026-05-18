# How To: Linearizelums Method 1

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test linearizeLums method 1

## Prerequisites

**Required Modules:**
- `os`
- `sys`
- `glob`
- `uuid`
- `psychopy.monitors.calibTools`
- `numpy`
- `pytest`


## Step-by-Step Guide

### Step 1: Assign m = Monitor(...)

```python
m = Monitor(name='foo')
```

**Verification:**
```python
assert np.allclose(r, desired_lums)
```

### Step 2: Assign unknown = 1

```python
m.currentCalib['gamma'] = 1
```

### Step 3: Assign unknown = 1

```python
m.currentCalib['linearizeMethod'] = 1
```

### Step 4: Assign desired_lums = np.array(...)

```python
desired_lums = np.array([0.1, 0.2, 0.3])
```

### Step 5: Assign r = m.linearizeLums(...)

```python
r = m.linearizeLums(desiredLums=desired_lums)
```

**Verification:**
```python
assert np.allclose(r, desired_lums)
```


## Complete Example

```python
# Workflow
m = Monitor(name='foo')
m.currentCalib['gamma'] = 1
m.currentCalib['linearizeMethod'] = 1
desired_lums = np.array([0.1, 0.2, 0.3])
r = m.linearizeLums(desiredLums=desired_lums)
assert np.allclose(r, desired_lums)
```

## Next Steps


---

*Source: test_monitors.py:62 | Complexity: Intermediate | Last updated: 2026-05-18*