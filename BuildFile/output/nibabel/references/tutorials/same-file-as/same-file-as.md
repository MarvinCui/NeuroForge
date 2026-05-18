# How To: Same File As

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test same file as

## Prerequisites

**Required Modules:**
- `io`
- `fileholders`


## Step-by-Step Guide

### Step 1: Assign fh = FileHolder(...)

```python
fh = FileHolder('a_fname')
```

**Verification:**
```python
assert fh.same_file_as(fh)
```

### Step 2: Assign fh2 = FileHolder(...)

```python
fh2 = FileHolder('a_test')
```

**Verification:**
```python
assert not fh.same_file_as(fh2)
```

### Step 3: Assign sio0 = BytesIO(...)

```python
sio0 = BytesIO()
```

**Verification:**
```python
assert fh3.same_file_as(fh4)
```

### Step 4: Assign fh3 = FileHolder(...)

```python
fh3 = FileHolder('a_fname', sio0)
```

**Verification:**
```python
assert not fh3.same_file_as(fh)
```

### Step 5: Assign fh4 = FileHolder(...)

```python
fh4 = FileHolder('a_fname', sio0)
```

**Verification:**
```python
assert fh5.same_file_as(fh6)
```

### Step 6: Assign fh5 = FileHolder(...)

```python
fh5 = FileHolder(fileobj=sio0)
```

**Verification:**
```python
assert not fh5.same_file_as(fh3)
```

### Step 7: Assign fh6 = FileHolder(...)

```python
fh6 = FileHolder(fileobj=sio0)
```

**Verification:**
```python
assert fh3.same_file_as(fh4_again)
```

### Step 8: Assign fh4_again = FileHolder(...)

```python
fh4_again = FileHolder('a_fname', sio0, pos=4)
```

**Verification:**
```python
assert fh3.same_file_as(fh4_again)
```


## Complete Example

```python
# Workflow
fh = FileHolder('a_fname')
assert fh.same_file_as(fh)
fh2 = FileHolder('a_test')
assert not fh.same_file_as(fh2)
sio0 = BytesIO()
fh3 = FileHolder('a_fname', sio0)
fh4 = FileHolder('a_fname', sio0)
assert fh3.same_file_as(fh4)
assert not fh3.same_file_as(fh)
fh5 = FileHolder(fileobj=sio0)
fh6 = FileHolder(fileobj=sio0)
assert fh5.same_file_as(fh6)
assert not fh5.same_file_as(fh3)
fh4_again = FileHolder('a_fname', sio0, pos=4)
assert fh3.same_file_as(fh4_again)
```

## Next Steps


---

*Source: test_fileholders.py:24 | Complexity: Advanced | Last updated: 2026-05-18*