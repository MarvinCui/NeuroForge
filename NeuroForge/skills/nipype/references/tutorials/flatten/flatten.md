# How To: Flatten

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test flatten

## Prerequisites

**Required Modules:**
- `os`
- `shutil`
- `pytest`
- `nipype.utils.misc`
- `misc`


## Step-by-Step Guide

### Step 1: Assign in_list = value

```python
in_list = [[1, 2, 3], [4], [[5, 6], 7], 8]
```

**Verification:**
```python
assert flat == [1, 2, 3, 4, 5, 6, 7, 8]
```

### Step 2: Assign flat = flatten(...)

```python
flat = flatten(in_list)
```

**Verification:**
```python
assert in_list == back
```

### Step 3: Assign back = unflatten(...)

```python
back = unflatten(flat, in_list)
```

**Verification:**
```python
assert back == [[2, 3, 4], [5], [[6, 7], 8], 9]
```

### Step 4: Assign new_list = value

```python
new_list = [2, 3, 4, 5, 6, 7, 8, 9]
```

**Verification:**
```python
assert flat == []
```

### Step 5: Assign back = unflatten(...)

```python
back = unflatten(new_list, in_list)
```

**Verification:**
```python
assert back == []
```

### Step 6: Assign flat = flatten(...)

```python
flat = flatten([])
```

**Verification:**
```python
assert flat == []
```

### Step 7: Assign back = unflatten(...)

```python
back = unflatten([], [])
```

**Verification:**
```python
assert back == []
```


## Complete Example

```python
# Workflow
in_list = [[1, 2, 3], [4], [[5, 6], 7], 8]
flat = flatten(in_list)
assert flat == [1, 2, 3, 4, 5, 6, 7, 8]
back = unflatten(flat, in_list)
assert in_list == back
new_list = [2, 3, 4, 5, 6, 7, 8, 9]
back = unflatten(new_list, in_list)
assert back == [[2, 3, 4], [5], [[6, 7], 8], 9]
flat = flatten([])
assert flat == []
back = unflatten([], [])
assert back == []
```

## Next Steps


---

*Source: test_misc.py:57 | Complexity: Intermediate | Last updated: 2026-05-18*