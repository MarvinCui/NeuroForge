# How To: Annotation Concat

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test if two Annotations objects can be concatenated.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `sys`
- `collections`
- `datetime`
- `itertools`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `pytest`
- `mne`
- `mne`
- `mne.annotations`
- `mne.datasets`
- `mne.io`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: with_extras
```

## Step-by-Step Guide

### Step 1: 'Test if two Annotations objects can be concatenated.'

```python
'Test if two Annotations objects can be concatenated.'
```

**Verification:**
```python
assert_array_equal(c.onset, [1, 2, 3, 11, 12, 13])
```

### Step 2: Assign extras = None

```python
extras = None
```

**Verification:**
```python
assert_array_equal(c.duration, [5, 5, 8, 1, 2, 2])
```

### Step 3: Assign a = Annotations(...)

```python
a = Annotations([1, 2, 3], [5, 5, 8], ['a', 'b', 'c'], ch_names=[['1'], ['2'], []])
```

**Verification:**
```python
assert_array_equal(c.description, ['a', 'b', 'c', 'x', 'y', 'z'])
```

### Step 4: Assign b = Annotations(...)

```python
b = Annotations([11, 12, 13], [1, 2, 2], ['x', 'y', 'z'], ch_names=[[], ['3'], []], extras=extras)
```

**Verification:**
```python
assert_equal(len(a), 3)
```

### Step 5: Assign c = value

```python
c = a + b
```

**Verification:**
```python
assert_equal(len(b), 3)
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(c.onset, [1, 2, 3, 11, 12, 13])
```

**Verification:**
```python
assert_equal(len(c), 6)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(c.duration, [5, 5, 8, 1, 2, 2])
```

**Verification:**
```python
assert_array_equal(c.ch_names, want_names)
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(c.description, ['a', 'b', 'c', 'x', 'y', 'z'])
```

**Verification:**
```python
assert_array_equal(a.onset, [1, 2, 3, 11, 12, 13])
```

### Step 9: Call assert_equal()

```python
assert_equal(len(a), 3)
```

**Verification:**
```python
assert_array_equal(a.duration, [5, 5, 8, 1, 2, 2])
```

### Step 10: Call assert_equal()

```python
assert_equal(len(b), 3)
```

**Verification:**
```python
assert_array_equal(a.description, ['a', 'b', 'c', 'x', 'y', 'z'])
```

### Step 11: Call assert_equal()

```python
assert_equal(len(c), 6)
```

**Verification:**
```python
assert_equal(len(a), 6)
```

### Step 12: Assign want_names = np.array(...)

```python
want_names = np.array([('1',), ('2',), (), (), ('3',), ()], dtype='O')
```

**Verification:**
```python
assert_equal(len(b), 3)
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(c.ch_names, want_names)
```

**Verification:**
```python
assert all((c.extras[i] == all_extras[i] for i in range(len(all_extras))))
```

### Step 14: Call assert_array_equal()

```python
assert_array_equal(a.onset, [1, 2, 3, 11, 12, 13])
```

### Step 15: Call assert_array_equal()

```python
assert_array_equal(a.duration, [5, 5, 8, 1, 2, 2])
```

### Step 16: Call assert_array_equal()

```python
assert_array_equal(a.description, ['a', 'b', 'c', 'x', 'y', 'z'])
```

### Step 17: Call assert_equal()

```python
assert_equal(len(a), 6)
```

### Step 18: Call assert_equal()

```python
assert_equal(len(b), 3)
```

### Step 19: Assign b._orig_time = _handle_meas_date(...)

```python
b._orig_time = _handle_meas_date(1038942070.7201)
```

### Step 20: Assign extras = value

```python
extras = [{'foo1': 1, 'foo2': 1.1, 'foo3': 'a', 'foo4': None}, None, None]
```

### Step 21: Assign all_extras = value

```python
all_extras = [extra or {} for extra in [None] * 3 + extras]
```

**Verification:**
```python
assert all((c.extras[i] == all_extras[i] for i in range(len(all_extras))))
```


## Complete Example

```python
# Setup
# Fixtures: with_extras

# Workflow
'Test if two Annotations objects can be concatenated.'
extras = None
if with_extras:
    extras = [{'foo1': 1, 'foo2': 1.1, 'foo3': 'a', 'foo4': None}, None, None]
a = Annotations([1, 2, 3], [5, 5, 8], ['a', 'b', 'c'], ch_names=[['1'], ['2'], []])
b = Annotations([11, 12, 13], [1, 2, 2], ['x', 'y', 'z'], ch_names=[[], ['3'], []], extras=extras)
c = a + b
assert_array_equal(c.onset, [1, 2, 3, 11, 12, 13])
assert_array_equal(c.duration, [5, 5, 8, 1, 2, 2])
assert_array_equal(c.description, ['a', 'b', 'c', 'x', 'y', 'z'])
assert_equal(len(a), 3)
assert_equal(len(b), 3)
assert_equal(len(c), 6)
want_names = np.array([('1',), ('2',), (), (), ('3',), ()], dtype='O')
assert_array_equal(c.ch_names, want_names)
a += b
assert_array_equal(a.onset, [1, 2, 3, 11, 12, 13])
assert_array_equal(a.duration, [5, 5, 8, 1, 2, 2])
assert_array_equal(a.description, ['a', 'b', 'c', 'x', 'y', 'z'])
assert_equal(len(a), 6)
assert_equal(len(b), 3)
if with_extras:
    all_extras = [extra or {} for extra in [None] * 3 + extras]
    assert all((c.extras[i] == all_extras[i] for i in range(len(all_extras))))
b._orig_time = _handle_meas_date(1038942070.7201)
with pytest.raises(ValueError, match='orig_time should be the same'):
    a += b
```

## Next Steps


---

*Source: test_annotations.py:637 | Complexity: Advanced | Last updated: 2026-05-18*