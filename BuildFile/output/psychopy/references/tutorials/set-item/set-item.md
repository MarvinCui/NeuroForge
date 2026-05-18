# How To: Set Item

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check that items in an IndexDict can be set as expected, should set by position only if the 
positional index is not already defined as an explicit key.

## Prerequisites

**Required Modules:**
- `psychopy.tools`
- `pytest`
- `numpy`


## Step-by-Step Guide

### Step 1: '\n        Check that items in an IndexDict can be set as expected, should set by position only if the \n        positional index is not already defined as an explicit key.\n        '

```python
'\n        Check that items in an IndexDict can be set as expected, should set by position only if the \n        positional index is not already defined as an explicit key.\n        '
```

**Verification:**
```python
assert self.data[geti] == getval, f'After setting data[{repr(seti)}] = {repr(setval)} expected to get data[{repr(geti)}] == {repr(getval)}, but instead got data[{repr(geti)}] == {repr(self.data[geti])}'
```

### Step 2: Assign cases = value

```python
cases = [{'set': (0, 'mno'), 'get': (0, 'mno')}, {'set': (0, 'mno'), 'get': ('someKey', 'mno')}, {'set': ('someKey', 'mno'), 'get': (0, 'mno')}, {'set': ('someKey', 'mno'), 'get': ('someKey', 'mno')}, {'set': ('someOtherKey', 'pqr'), 'get': ('someOtherKey', 'pqr')}, {'set': ('someOtherKey', 'mno'), 'get': (1, 'jkl')}, {'set': (1, 'pqr'), 'get': ('someOtherKey', 'def')}, {'set': (1, 'pqr'), 'get': (1, 'pqr')}, {'set': ('newKey', 'stu'), 'get': ('newKey', 'stu')}, {'set': ('newKey', 'stu'), 'get': (4, 'stu')}, {'set': (6, 'stu'), 'get': (6, 'stu')}]
```

### Step 3: Call self.recreateData()

```python
self.recreateData()
```

### Step 4: Assign unknown = value

```python
seti, setval = case['set']
```

### Step 5: Assign unknown = value

```python
geti, getval = case['get']
```

### Step 6: Assign unknown = setval

```python
self.data[seti] = setval
```

**Verification:**
```python
assert self.data[geti] == getval, f'After setting data[{repr(seti)}] = {repr(setval)} expected to get data[{repr(geti)}] == {repr(getval)}, but instead got data[{repr(geti)}] == {repr(self.data[geti])}'
```


## Complete Example

```python
# Workflow
'\n        Check that items in an IndexDict can be set as expected, should set by position only if the \n        positional index is not already defined as an explicit key.\n        '
cases = [{'set': (0, 'mno'), 'get': (0, 'mno')}, {'set': (0, 'mno'), 'get': ('someKey', 'mno')}, {'set': ('someKey', 'mno'), 'get': (0, 'mno')}, {'set': ('someKey', 'mno'), 'get': ('someKey', 'mno')}, {'set': ('someOtherKey', 'pqr'), 'get': ('someOtherKey', 'pqr')}, {'set': ('someOtherKey', 'mno'), 'get': (1, 'jkl')}, {'set': (1, 'pqr'), 'get': ('someOtherKey', 'def')}, {'set': (1, 'pqr'), 'get': (1, 'pqr')}, {'set': ('newKey', 'stu'), 'get': ('newKey', 'stu')}, {'set': ('newKey', 'stu'), 'get': (4, 'stu')}, {'set': (6, 'stu'), 'get': (6, 'stu')}]
for case in cases:
    self.recreateData()
    seti, setval = case['set']
    geti, getval = case['get']
    self.data[seti] = setval
    assert self.data[geti] == getval, f'After setting data[{repr(seti)}] = {repr(setval)} expected to get data[{repr(geti)}] == {repr(getval)}, but instead got data[{repr(geti)}] == {repr(self.data[geti])}'
```

## Next Steps


---

*Source: test_arraytools.py:213 | Complexity: Intermediate | Last updated: 2026-05-18*