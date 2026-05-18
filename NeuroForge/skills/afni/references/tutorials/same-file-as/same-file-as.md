# How To: Same File As

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test same file as

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
assert_true(fh.same_file_as(fh))
```

### Step 2: Call assert_true()

```python
assert_true(fh.same_file_as(fh))
```

**Verification:**
```python
assert_false(fh.same_file_as(fh2))
```

### Step 3: Assign fh2 = FileHolder(...)

```python
fh2 = FileHolder('a_test')
```

**Verification:**
```python
assert_true(fh3.same_file_as(fh4))
```

### Step 4: Call assert_false()

```python
assert_false(fh.same_file_as(fh2))
```

**Verification:**
```python
assert_false(fh3.same_file_as(fh))
```

### Step 5: Assign sio0 = StringIO(...)

```python
sio0 = StringIO()
```

**Verification:**
```python
assert_true(fh5.same_file_as(fh6))
```

### Step 6: Assign fh3 = FileHolder(...)

```python
fh3 = FileHolder('a_fname', sio0)
```

**Verification:**
```python
assert_false(fh5.same_file_as(fh3))
```

### Step 7: Assign fh4 = FileHolder(...)

```python
fh4 = FileHolder('a_fname', sio0)
```

**Verification:**
```python
assert_true(fh3.same_file_as(fh4_again))
```

### Step 8: Call assert_true()

```python
assert_true(fh3.same_file_as(fh4))
```

### Step 9: Call assert_false()

```python
assert_false(fh3.same_file_as(fh))
```

### Step 10: Assign fh5 = FileHolder(...)

```python
fh5 = FileHolder(fileobj=sio0)
```

### Step 11: Assign fh6 = FileHolder(...)

```python
fh6 = FileHolder(fileobj=sio0)
```

### Step 12: Call assert_true()

```python
assert_true(fh5.same_file_as(fh6))
```

### Step 13: Call assert_false()

```python
assert_false(fh5.same_file_as(fh3))
```

### Step 14: Assign fh4_again = FileHolder(...)

```python
fh4_again = FileHolder('a_fname', sio0, pos=4)
```

### Step 15: Call assert_true()

```python
assert_true(fh3.same_file_as(fh4_again))
```


## Complete Example

```python
# Workflow
fh = FileHolder('a_fname')
assert_true(fh.same_file_as(fh))
fh2 = FileHolder('a_test')
assert_false(fh.same_file_as(fh2))
sio0 = StringIO()
fh3 = FileHolder('a_fname', sio0)
fh4 = FileHolder('a_fname', sio0)
assert_true(fh3.same_file_as(fh4))
assert_false(fh3.same_file_as(fh))
fh5 = FileHolder(fileobj=sio0)
fh6 = FileHolder(fileobj=sio0)
assert_true(fh5.same_file_as(fh6))
assert_false(fh5.same_file_as(fh3))
fh4_again = FileHolder('a_fname', sio0, pos=4)
assert_true(fh3.same_file_as(fh4_again))
```

## Next Steps


---

*Source: test_fileholders.py:33 | Complexity: Advanced | Last updated: 2026-05-18*