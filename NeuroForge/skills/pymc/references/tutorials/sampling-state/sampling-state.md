# How To: Sampling State

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test sampling state

## Prerequisites

**Required Modules:**
- `dataclasses`
- `numpy`
- `pytest`
- `pymc.step_methods.state`
- `tests.helpers`


## Step-by-Step Guide

### Step 1: Assign b1 = B(...)

```python
b1 = B()
```

**Verification:**
```python
assert equal_sampling_states(b1_state.state1, b2_state.state1)
```

### Step 2: Assign b2 = B(...)

```python
b2 = B(mutable_field=2.0)
```

**Verification:**
```python
assert not equal_sampling_states(b1_state, b2_state)
```

### Step 3: Assign b3 = B(...)

```python
b3 = B(c=1, extra_info1=np.array([10, 20]))
```

**Verification:**
```python
assert not equal_sampling_states(b1_state, b3_state)
```

### Step 4: Assign b4 = B(...)

```python
b4 = B(a=2, b=3.0, c='d')
```

**Verification:**
```python
assert not equal_sampling_states(b1_state, b4_state)
```

### Step 5: Assign b5 = B(...)

```python
b5 = B(c=1)
```

**Verification:**
```python
assert equal_sampling_states(b1.sampling_state, b2_state)
```

### Step 6: Assign b6 = B(...)

```python
b6 = B(f={'a': 1, 'b': 'c', 'd': None})
```

**Verification:**
```python
assert equal_sampling_states(b1.sampling_state, b4_state)
```

### Step 7: Assign b1_state = value

```python
b1_state = b1.sampling_state
```

**Verification:**
```python
assert not equal_sampling_states(b1.sampling_state, b5.sampling_state)
```

### Step 8: Assign b2_state = value

```python
b2_state = b2.sampling_state
```

**Verification:**
```python
assert not equal_sampling_states(b1.sampling_state, b6.sampling_state)
```

### Step 9: Assign b3_state = value

```python
b3_state = b3.sampling_state
```

### Step 10: Assign b4_state = value

```python
b4_state = b4.sampling_state
```

**Verification:**
```python
assert equal_sampling_states(b1_state.state1, b2_state.state1)
```

### Step 11: Assign b1.sampling_state = b2_state

```python
b1.sampling_state = b2_state
```

**Verification:**
```python
assert equal_sampling_states(b1.sampling_state, b2_state)
```

### Step 12: Assign expected_error_message = "The received sampling state must have the same values for the frozen fields. Field 'extra_info1' has different values. Expected \\[3 4 5\\] but got \\[10 20\\]"

```python
expected_error_message = "The received sampling state must have the same values for the frozen fields. Field 'extra_info1' has different values. Expected \\[3 4 5\\] but got \\[10 20\\]"
```

### Step 13: Assign b1.sampling_state = b4_state

```python
b1.sampling_state = b4_state
```

**Verification:**
```python
assert equal_sampling_states(b1.sampling_state, b4_state)
```

### Step 14: Assign b1.sampling_state = b3_state

```python
b1.sampling_state = b3_state
```

### Step 15: Assign b1.sampling_state = value

```python
b1.sampling_state = b1_state.state1
```


## Complete Example

```python
# Workflow
b1 = B()
b2 = B(mutable_field=2.0)
b3 = B(c=1, extra_info1=np.array([10, 20]))
b4 = B(a=2, b=3.0, c='d')
b5 = B(c=1)
b6 = B(f={'a': 1, 'b': 'c', 'd': None})
b1_state = b1.sampling_state
b2_state = b2.sampling_state
b3_state = b3.sampling_state
b4_state = b4.sampling_state
assert equal_sampling_states(b1_state.state1, b2_state.state1)
assert not equal_sampling_states(b1_state, b2_state)
assert not equal_sampling_states(b1_state, b3_state)
assert not equal_sampling_states(b1_state, b4_state)
b1.sampling_state = b2_state
assert equal_sampling_states(b1.sampling_state, b2_state)
expected_error_message = "The received sampling state must have the same values for the frozen fields. Field 'extra_info1' has different values. Expected \\[3 4 5\\] but got \\[10 20\\]"
with pytest.raises(ValueError, match=expected_error_message):
    b1.sampling_state = b3_state
with pytest.raises(AssertionError, match='Encountered invalid state class'):
    b1.sampling_state = b1_state.state1
b1.sampling_state = b4_state
assert equal_sampling_states(b1.sampling_state, b4_state)
assert not equal_sampling_states(b1.sampling_state, b5.sampling_state)
assert not equal_sampling_states(b1.sampling_state, b6.sampling_state)
```

## Next Steps


---

*Source: test_state.py:101 | Complexity: Advanced | Last updated: 2026-05-18*