# How To: File Like

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test file like

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
assert fh.file_like == 'a_fname'
```

### Step 2: Assign bio = BytesIO(...)

```python
bio = BytesIO()
```

**Verification:**
```python
assert fh.file_like is bio
```

### Step 3: Assign fh = FileHolder(...)

```python
fh = FileHolder(fileobj=bio)
```

**Verification:**
```python
assert fh.file_like is bio
```

### Step 4: Assign fh = FileHolder(...)

```python
fh = FileHolder('a_fname', fileobj=bio)
```

**Verification:**
```python
assert fh.file_like is bio
```


## Complete Example

```python
# Workflow
fh = FileHolder('a_fname')
assert fh.file_like == 'a_fname'
bio = BytesIO()
fh = FileHolder(fileobj=bio)
assert fh.file_like is bio
fh = FileHolder('a_fname', fileobj=bio)
assert fh.file_like is bio
```

## Next Steps


---

*Source: test_fileholders.py:44 | Complexity: Intermediate | Last updated: 2026-05-18*