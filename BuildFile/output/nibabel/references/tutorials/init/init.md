# How To: Init

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test init

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
assert fh.filename == 'a_fname'
```

### Step 2: Assign sio0 = BytesIO(...)

```python
sio0 = BytesIO()
```

**Verification:**
```python
assert fh.fileobj is None
```

### Step 3: Assign fh = FileHolder(...)

```python
fh = FileHolder('a_test', sio0)
```

**Verification:**
```python
assert fh.pos == 0
```

### Step 4: Assign fh = FileHolder(...)

```python
fh = FileHolder('a_test_2', sio0, 3)
```

**Verification:**
```python
assert fh.filename == 'a_test'
```


## Complete Example

```python
# Workflow
fh = FileHolder('a_fname')
assert fh.filename == 'a_fname'
assert fh.fileobj is None
assert fh.pos == 0
sio0 = BytesIO()
fh = FileHolder('a_test', sio0)
assert fh.filename == 'a_test'
assert fh.fileobj is sio0
assert fh.pos == 0
fh = FileHolder('a_test_2', sio0, 3)
assert fh.filename == 'a_test_2'
assert fh.fileobj is sio0
assert fh.pos == 3
```

## Next Steps


---

*Source: test_fileholders.py:8 | Complexity: Intermediate | Last updated: 2026-05-18*