# How To: Determine Num Processes

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test determine num processes

## Prerequisites

**Required Modules:**
- `numpy.testing`
- `dipy.utils.multiproc`


## Step-by-Step Guide

### Step 1: Call assert_raises()

```python
assert_raises(ValueError, determine_num_processes, 0)
```

**Verification:**
```python
assert_raises(ValueError, determine_num_processes, 0)
```

### Step 2: Call assert_raises()

```python
assert_raises(TypeError, determine_num_processes, '0')
```

**Verification:**
```python
assert_raises(TypeError, determine_num_processes, '0')
```

### Step 3: Call assert_equal()

```python
assert_equal(determine_num_processes(1), 1)
```

**Verification:**
```python
assert_equal(determine_num_processes(1), 1)
```

### Step 4: Call assert_equal()

```python
assert_equal(determine_num_processes(4), 4)
```

**Verification:**
```python
assert_equal(determine_num_processes(4), 4)
```

### Step 5: Call assert_equal()

```python
assert_equal(determine_num_processes(None), determine_num_processes(-1))
```

**Verification:**
```python
assert_equal(determine_num_processes(None), determine_num_processes(-1))
```

### Step 6: Call assert_equal()

```python
assert_equal(determine_num_processes(-10000), 1)
```

**Verification:**
```python
assert_equal(determine_num_processes(-10000), 1)
```

### Step 7: Call assert_equal()

```python
assert_equal(determine_num_processes(-1), determine_num_processes(-2) + 1)
```

**Verification:**
```python
assert_equal(determine_num_processes(-1), determine_num_processes(-2) + 1)
```


## Complete Example

```python
# Workflow
assert_raises(ValueError, determine_num_processes, 0)
assert_raises(TypeError, determine_num_processes, '0')
assert_equal(determine_num_processes(1), 1)
assert_equal(determine_num_processes(4), 4)
assert_equal(determine_num_processes(None), determine_num_processes(-1))
assert_equal(determine_num_processes(-10000), 1)
if determine_num_processes(-1) > 1:
    assert_equal(determine_num_processes(-1), determine_num_processes(-2) + 1)
```

## Next Steps


---

*Source: test_multiproc.py:8 | Complexity: Intermediate | Last updated: 2026-05-18*