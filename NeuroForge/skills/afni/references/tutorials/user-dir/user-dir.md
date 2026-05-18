# How To: User Dir

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test user dir

## Prerequisites

**Required Modules:**
- `os`
- `os`
- `os.path`
- `sys`
- `numpy`
- `numpy.testing`
- `nose.tools`
- `nose`


## Step-by-Step Guide

### Step 1: Assign home_dir = nibe.get_home_dir(...)

```python
home_dir = nibe.get_home_dir()
```

**Verification:**
```python
assert_equal(exp, nibe.get_nipy_user_dir())
```

### Step 2: Call assert_equal()

```python
assert_equal(exp, nibe.get_nipy_user_dir())
```

**Verification:**
```python
assert_equal(abspath('/a/path'), nibe.get_nipy_user_dir())
```

### Step 3: Assign unknown = '/a/path'

```python
env[USER_KEY] = '/a/path'
```

### Step 4: Call assert_equal()

```python
assert_equal(abspath('/a/path'), nibe.get_nipy_user_dir())
```

### Step 5: Assign exp = pjoin(...)

```python
exp = pjoin(home_dir, '.nipy')
```

### Step 6: Assign exp = pjoin(...)

```python
exp = pjoin(home_dir, '_nipy')
```


## Complete Example

```python
# Workflow
if USER_KEY in env:
    del env[USER_KEY]
home_dir = nibe.get_home_dir()
if os.name == 'posix':
    exp = pjoin(home_dir, '.nipy')
else:
    exp = pjoin(home_dir, '_nipy')
assert_equal(exp, nibe.get_nipy_user_dir())
env[USER_KEY] = '/a/path'
assert_equal(abspath('/a/path'), nibe.get_nipy_user_dir())
```

## Next Steps


---

*Source: test_environment.py:56 | Complexity: Intermediate | Last updated: 2026-05-18*