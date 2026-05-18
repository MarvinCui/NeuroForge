# How To: Pickle

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test if BunchConstNamed object can be pickled.

## Prerequisites

**Required Modules:**
- `pickle`
- `mne.utils`
- `mne.utils._bunch`


## Step-by-Step Guide

### Step 1: 'Test if BunchConstNamed object can be pickled.'

```python
'Test if BunchConstNamed object can be pickled.'
```

**Verification:**
```python
assert isinstance(b1.x, int)
```

### Step 2: Assign b1 = BunchConstNamed(...)

```python
b1 = BunchConstNamed()
```

**Verification:**
```python
assert isinstance(b1.x, NamedInt)
```

### Step 3: Assign b1.x = 1

```python
b1.x = 1
```

**Verification:**
```python
assert repr(b1.x) == '1 (x)'
```

### Step 4: Assign b1.y = 2.12

```python
b1.y = 2.12
```

**Verification:**
```python
assert isinstance(b1.y, float)
```

### Step 5: Assign b2 = pickle.loads(...)

```python
b2 = pickle.loads(pickle.dumps(b1))
```

**Verification:**
```python
assert isinstance(b1.y, NamedFloat)
```


## Complete Example

```python
# Workflow
'Test if BunchConstNamed object can be pickled.'
b1 = BunchConstNamed()
b1.x = 1
b1.y = 2.12
assert isinstance(b1.x, int)
assert isinstance(b1.x, NamedInt)
assert repr(b1.x) == '1 (x)'
assert isinstance(b1.y, float)
assert isinstance(b1.y, NamedFloat)
assert repr(b1.y) == '2.12 (y)'
b2 = pickle.loads(pickle.dumps(b1))
assert b1 == b2
```

## Next Steps


---

*Source: test_bunch.py:11 | Complexity: Intermediate | Last updated: 2026-05-18*