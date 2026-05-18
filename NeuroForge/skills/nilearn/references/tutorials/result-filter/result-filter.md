# How To: Result Filter

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test ResultFilter IsIn NotIn.

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

### Step 1: 'Test ResultFilter IsIn NotIn.'

```python
'Test ResultFilter IsIn NotIn.'
```

**Verification:**
```python
assert str(filter_0) == 'ResultFilter'
```

### Step 2: Assign filter_0 = neurovault.ResultFilter(...)

```python
filter_0 = neurovault.ResultFilter(query_terms={'a': 0}, callable_filter=lambda d: len(d) < 5, b=1)
```

**Verification:**
```python
assert filter_0['a'] == 0
```

### Step 3: Assign filter_1 = neurovault.ResultFilter(...)

```python
filter_1 = neurovault.ResultFilter(query_terms={'c': 2})
```

**Verification:**
```python
assert filter_0({'a': 0, 'b': 1, 'c': 2})
```

### Step 4: Assign unknown = neurovault.NotNull(...)

```python
filter_1['d'] = neurovault.NotNull()
```

**Verification:**
```python
assert not filter_0({'a': 0, 'b': 1, 'c': 2, 'd': 3, 'e': 4})
```

### Step 5: Assign unknown = neurovault.IsIn(...)

```python
filter_1['d'] = neurovault.IsIn(0, 1)
```

**Verification:**
```python
assert not filter_0({'b': 1, 'c': 2, 'd': 3})
```

### Step 6: Assign unknown = neurovault.NotIn(...)

```python
filter_1['d'] = neurovault.NotIn(0, 1)
```

**Verification:**
```python
assert not filter_0({'a': 1, 'b': 1, 'c': 2})
```

### Step 7: Call filter_1.add_filter()

```python
filter_1.add_filter(lambda d: len(d) > 2)
```

**Verification:**
```python
assert filter_1({'c': 2, 'd': 1})
```


## Complete Example

```python
# Workflow
'Test ResultFilter IsIn NotIn.'
filter_0 = neurovault.ResultFilter(query_terms={'a': 0}, callable_filter=lambda d: len(d) < 5, b=1)
assert str(filter_0) == 'ResultFilter'
assert filter_0['a'] == 0
assert filter_0({'a': 0, 'b': 1, 'c': 2})
assert not filter_0({'a': 0, 'b': 1, 'c': 2, 'd': 3, 'e': 4})
assert not filter_0({'b': 1, 'c': 2, 'd': 3})
assert not filter_0({'a': 1, 'b': 1, 'c': 2})
filter_1 = neurovault.ResultFilter(query_terms={'c': 2})
filter_1['d'] = neurovault.NotNull()
assert filter_1({'c': 2, 'd': 1})
assert not filter_1({'c': 2, 'd': 0})
filter_1['d'] = neurovault.IsIn(0, 1)
assert filter_1({'c': 2, 'd': 1})
assert not filter_1({'c': 2, 'd': 2})
del filter_1['d']
assert filter_1({'c': 2, 'd': 2})
filter_1['d'] = neurovault.NotIn(0, 1)
assert not filter_1({'c': 2, 'd': 1})
assert filter_1({'c': 2, 'd': 3})
filter_1.add_filter(lambda d: len(d) > 2)
assert not filter_1({'c': 2, 'd': 3})
assert filter_1({'c': 2, 'd': 3, 'e': 4})
```

## Next Steps


---

*Source: test_neurovault.py:466 | Complexity: Intermediate | Last updated: 2026-05-18*