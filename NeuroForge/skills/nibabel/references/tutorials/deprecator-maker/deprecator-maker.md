# How To: Deprecator Maker

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test deprecator maker

## Prerequisites

**Required Modules:**
- `sys`
- `warnings`
- `functools`
- `textwrap`
- `pytest`
- `nibabel.deprecator`
- `testing`


## Step-by-Step Guide

### Step 1: Assign dec = self.dep_maker(...)

```python
dec = self.dep_maker(warn_class=UserWarning)
```

**Verification:**
```python
assert func() is None
```

### Step 2: Assign func = dec(...)

```python
func = dec('foo')(func_no_doc)
```

**Verification:**
```python
assert len(w) == 1
```

### Step 3: Assign dec = self.dep_maker(...)

```python
dec = self.dep_maker(error_class=CustomError)
```

**Verification:**
```python
assert func() is None
```

### Step 4: Assign func = dec(...)

```python
func = dec('foo')(func_no_doc)
```

### Step 5: Assign func = dec(...)

```python
func = dec('foo', until='1.8')(func_no_doc)
```

**Verification:**
```python
assert func() is None
```

### Step 6: Call func()

```python
func()
```


## Complete Example

```python
# Workflow
dec = self.dep_maker(warn_class=UserWarning)
func = dec('foo')(func_no_doc)
with pytest.warns(UserWarning) as w:
    assert func() is None
    assert len(w) == 1
dec = self.dep_maker(error_class=CustomError)
func = dec('foo')(func_no_doc)
with pytest.deprecated_call():
    assert func() is None
func = dec('foo', until='1.8')(func_no_doc)
with pytest.raises(CustomError):
    func()
```

## Next Steps


---

*Source: test_deprecator.py:166 | Complexity: Intermediate | Last updated: 2026-05-18*