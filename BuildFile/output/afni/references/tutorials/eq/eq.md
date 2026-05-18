# How To: Eq

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test eq

## Prerequisites

**Required Modules:**
- `py3k`
- `numpy`
- `spatialimages`
- `unittest`
- `nose.tools`
- `numpy.testing`


## Step-by-Step Guide

### Step 1: Assign hdr = Header(...)

```python
hdr = Header()
```

**Verification:**
```python
assert_equal(hdr, other)
```

### Step 2: Assign other = Header(...)

```python
other = Header()
```

**Verification:**
```python
assert_not_equal(hdr, other)
```

### Step 3: Call assert_equal()

```python
assert_equal(hdr, other)
```

**Verification:**
```python
assert_not_equal(hdr, other)
```

### Step 4: Assign other = Header(...)

```python
other = Header('u2')
```

**Verification:**
```python
assert_equal(hdr, other)
```

### Step 5: Call assert_not_equal()

```python
assert_not_equal(hdr, other)
```

**Verification:**
```python
assert_not_equal(hdr, other)
```

### Step 6: Assign other = Header(...)

```python
other = Header(shape=(1, 2, 3))
```

### Step 7: Call assert_not_equal()

```python
assert_not_equal(hdr, other)
```

### Step 8: Assign hdr = Header(...)

```python
hdr = Header(shape=(1, 2))
```

### Step 9: Assign other = Header(...)

```python
other = Header(shape=(1, 2))
```

### Step 10: Call assert_equal()

```python
assert_equal(hdr, other)
```

### Step 11: Assign other = Header(...)

```python
other = Header(shape=(1, 2), zooms=(2.0, 3.0))
```

### Step 12: Call assert_not_equal()

```python
assert_not_equal(hdr, other)
```


## Complete Example

```python
# Workflow
hdr = Header()
other = Header()
assert_equal(hdr, other)
other = Header('u2')
assert_not_equal(hdr, other)
other = Header(shape=(1, 2, 3))
assert_not_equal(hdr, other)
hdr = Header(shape=(1, 2))
other = Header(shape=(1, 2))
assert_equal(hdr, other)
other = Header(shape=(1, 2), zooms=(2.0, 3.0))
assert_not_equal(hdr, other)
```

## Next Steps


---

*Source: test_spatialimages.py:73 | Complexity: Advanced | Last updated: 2026-05-18*