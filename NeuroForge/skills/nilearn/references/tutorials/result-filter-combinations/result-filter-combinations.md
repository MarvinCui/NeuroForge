# How To: Result Filter Combinations

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test ResultFilter AND OR XOR NOT.

## Prerequisites

**Required Modules:**
- `hashlib`
- `json`
- `os`
- `re`
- `stat`
- `pathlib`
- `urllib`
- `numpy`
- `pandas`
- `pytest`
- `requests`
- `nilearn._utils.data_gen`
- `nilearn.conftest`
- `nilearn.datasets`
- `nilearn.image`


## Step-by-Step Guide

### Step 1: 'Test ResultFilter AND OR XOR NOT.'

```python
'Test ResultFilter AND OR XOR NOT.'
```

**Verification:**
```python
assert filter_0_and_1({'a': 0, 'b': 1, 'c': 2, 'd': 3})
```

### Step 2: Assign filter_0 = neurovault.ResultFilter(...)

```python
filter_0 = neurovault.ResultFilter(a=0, b=1)
```

**Verification:**
```python
assert not filter_0_and_1({'a': 0, 'b': 1, 'c': 2, 'd': None})
```

### Step 3: Assign filter_1 = neurovault.ResultFilter(...)

```python
filter_1 = neurovault.ResultFilter(c=2, d=3)
```

**Verification:**
```python
assert not filter_0_and_1({'a': None, 'b': 1, 'c': 2, 'd': 3})
```

### Step 4: Assign filter_0_and_1 = filter_0.AND(...)

```python
filter_0_and_1 = filter_0.AND(filter_1)
```

**Verification:**
```python
assert filter_0_or_1({'a': 0, 'b': 1, 'c': 2, 'd': 3})
```

### Step 5: Assign filter_0_or_1 = filter_0.OR(...)

```python
filter_0_or_1 = filter_0.OR(filter_1)
```

**Verification:**
```python
assert filter_0_or_1({'a': 0, 'b': 1, 'c': 2, 'd': None})
```

### Step 6: Assign filter_0_xor_1 = filter_0.XOR(...)

```python
filter_0_xor_1 = filter_0.XOR(filter_1)
```

**Verification:**
```python
assert filter_0_or_1({'a': None, 'b': 1, 'c': 2, 'd': 3})
```

### Step 7: Assign not_filter_0 = filter_0.NOT(...)

```python
not_filter_0 = filter_0.NOT()
```

**Verification:**
```python
assert not filter_0_or_1({'a': None, 'b': 1, 'c': 2, 'd': None})
```

### Step 8: Assign filter_2 = neurovault.ResultFilter.AND(...)

```python
filter_2 = neurovault.ResultFilter({'a': neurovault.NotNull()}).AND(lambda d: len(d) < 2)
```

**Verification:**
```python
assert not filter_0_xor_1({'a': 0, 'b': 1, 'c': 2, 'd': 3})
```

### Step 9: Assign filt = neurovault.ResultFilter.AND(...)

```python
filt = neurovault.ResultFilter(a=0).AND(neurovault.ResultFilter(b=1).OR(neurovault.ResultFilter(b=2)))
```

**Verification:**
```python
assert filter_0_xor_1({'a': 0, 'b': 1, 'c': 2, 'd': None})
```


## Complete Example

```python
# Workflow
'Test ResultFilter AND OR XOR NOT.'
filter_0 = neurovault.ResultFilter(a=0, b=1)
filter_1 = neurovault.ResultFilter(c=2, d=3)
filter_0_and_1 = filter_0.AND(filter_1)
assert filter_0_and_1({'a': 0, 'b': 1, 'c': 2, 'd': 3})
assert not filter_0_and_1({'a': 0, 'b': 1, 'c': 2, 'd': None})
assert not filter_0_and_1({'a': None, 'b': 1, 'c': 2, 'd': 3})
filter_0_or_1 = filter_0.OR(filter_1)
assert filter_0_or_1({'a': 0, 'b': 1, 'c': 2, 'd': 3})
assert filter_0_or_1({'a': 0, 'b': 1, 'c': 2, 'd': None})
assert filter_0_or_1({'a': None, 'b': 1, 'c': 2, 'd': 3})
assert not filter_0_or_1({'a': None, 'b': 1, 'c': 2, 'd': None})
filter_0_xor_1 = filter_0.XOR(filter_1)
assert not filter_0_xor_1({'a': 0, 'b': 1, 'c': 2, 'd': 3})
assert filter_0_xor_1({'a': 0, 'b': 1, 'c': 2, 'd': None})
assert filter_0_xor_1({'a': None, 'b': 1, 'c': 2, 'd': 3})
assert not filter_0_xor_1({'a': None, 'b': 1, 'c': 2, 'd': None})
not_filter_0 = filter_0.NOT()
assert not_filter_0({})
assert not not_filter_0({'a': 0, 'b': 1})
filter_2 = neurovault.ResultFilter({'a': neurovault.NotNull()}).AND(lambda d: len(d) < 2)
assert filter_2({'a': 'a'})
assert not filter_2({'a': ''})
assert not filter_2({'a': 'a', 'b': 0})
filt = neurovault.ResultFilter(a=0).AND(neurovault.ResultFilter(b=1).OR(neurovault.ResultFilter(b=2)))
assert filt({'a': 0, 'b': 1})
assert not filt({'a': 0, 'b': 0})
```

## Next Steps


---

*Source: test_neurovault.py:505 | Complexity: Advanced | Last updated: 2026-05-18*