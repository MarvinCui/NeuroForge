# How To: Fname Presuffix

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test fname presuffix

## Prerequisites

**Required Modules:**
- `os`
- `time`
- `pathlib`
- `unittest`
- `pytest`
- `testing`
- `utils.filemanip`


## Step-by-Step Guide

### Step 1: Assign fname = 'foo.nii'

```python
fname = 'foo.nii'
```

**Verification:**
```python
assert pth == '/tmp/pre_foo_post.nii'
```

### Step 2: Assign pth = fname_presuffix(...)

```python
pth = fname_presuffix(fname, 'pre_', '_post', '/tmp')
```

**Verification:**
```python
assert pth == '/tmp/pre_foo_post.nii.gz'
```

### Step 3: Assign pth = fname_presuffix(...)

```python
pth = fname_presuffix(fname, 'pre_', '_post', '/tmp')
```

**Verification:**
```python
assert pth == '/tmp/pre_foo_post'
```

### Step 4: Assign pth = fname_presuffix(...)

```python
pth = fname_presuffix(fname, 'pre_', '_post', '/tmp', use_ext=False)
```

**Verification:**
```python
assert pth == '/tmp/pre_foo_post'
```


## Complete Example

```python
# Workflow
fname = 'foo.nii'
pth = fname_presuffix(fname, 'pre_', '_post', '/tmp')
assert pth == '/tmp/pre_foo_post.nii'
fname += '.gz'
pth = fname_presuffix(fname, 'pre_', '_post', '/tmp')
assert pth == '/tmp/pre_foo_post.nii.gz'
pth = fname_presuffix(fname, 'pre_', '_post', '/tmp', use_ext=False)
assert pth == '/tmp/pre_foo_post'
```

## Next Steps


---

*Source: test_filemanip.py:57 | Complexity: Intermediate | Last updated: 2026-05-18*