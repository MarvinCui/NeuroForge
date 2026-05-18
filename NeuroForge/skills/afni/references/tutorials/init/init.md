# How To: Init

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test init

## Prerequisites

**Required Modules:**
- `StringIO`
- `numpy`
- `fileholders`
- `tmpdirs`
- `numpy.testing`
- `nose.tools`


## Step-by-Step Guide

### Step 1: Assign fh = FileHolder(...)

```python
fh = FileHolder('a_fname')
```

**Verification:**
```python
assert_equal(fh.filename, 'a_fname')
```

### Step 2: Call assert_equal()

```python
assert_equal(fh.filename, 'a_fname')
```

**Verification:**
```python
assert_true(fh.fileobj is None)
```

### Step 3: Call assert_true()

```python
assert_true(fh.fileobj is None)
```

**Verification:**
```python
assert_equal(fh.pos, 0)
```

### Step 4: Call assert_equal()

```python
assert_equal(fh.pos, 0)
```

**Verification:**
```python
assert_equal(fh.filename, 'a_test')
```

### Step 5: Assign sio0 = StringIO(...)

```python
sio0 = StringIO()
```

**Verification:**
```python
assert_true(fh.fileobj is sio0)
```

### Step 6: Assign fh = FileHolder(...)

```python
fh = FileHolder('a_test', sio0)
```

**Verification:**
```python
assert_equal(fh.pos, 0)
```

### Step 7: Call assert_equal()

```python
assert_equal(fh.filename, 'a_test')
```

**Verification:**
```python
assert_equal(fh.filename, 'a_test_2')
```

### Step 8: Call assert_true()

```python
assert_true(fh.fileobj is sio0)
```

**Verification:**
```python
assert_true(fh.fileobj is sio0)
```

### Step 9: Call assert_equal()

```python
assert_equal(fh.pos, 0)
```

**Verification:**
```python
assert_equal(fh.pos, 3)
```

### Step 10: Assign fh = FileHolder(...)

```python
fh = FileHolder('a_test_2', sio0, 3)
```

### Step 11: Call assert_equal()

```python
assert_equal(fh.filename, 'a_test_2')
```

### Step 12: Call assert_true()

```python
assert_true(fh.fileobj is sio0)
```

### Step 13: Call assert_equal()

```python
assert_equal(fh.pos, 3)
```


## Complete Example

```python
# Workflow
fh = FileHolder('a_fname')
assert_equal(fh.filename, 'a_fname')
assert_true(fh.fileobj is None)
assert_equal(fh.pos, 0)
sio0 = StringIO()
fh = FileHolder('a_test', sio0)
assert_equal(fh.filename, 'a_test')
assert_true(fh.fileobj is sio0)
assert_equal(fh.pos, 0)
fh = FileHolder('a_test_2', sio0, 3)
assert_equal(fh.filename, 'a_test_2')
assert_true(fh.fileobj is sio0)
assert_equal(fh.pos, 3)
```

## Next Steps


---

*Source: test_fileholders.py:17 | Complexity: Advanced | Last updated: 2026-05-18*