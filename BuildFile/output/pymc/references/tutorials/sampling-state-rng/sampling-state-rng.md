# How To: Sampling State Rng

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test sampling state rng

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `dataclasses`
- `numpy`
- `pytest`
- `pymc.step_methods.state`
- `tests.helpers`

**Setup Required:**
```python
# Fixtures: step
```

## Step-by-Step Guide

### Step 1: Assign original_state = value

```python
original_state = step.sampling_state
```

**Verification:**
```python
assert not equal_sampling_states(original_state, final_state)
```

### Step 2: Assign values1 = step.rng.random(...)

```python
values1 = step.rng.random(100)
```

**Verification:**
```python
assert np.array_equal(values1, values2, equal_nan=True)
```

### Step 3: Assign final_state = value

```python
final_state = step.sampling_state
```

**Verification:**
```python
assert equal_sampling_states(step.sampling_state, final_state)
```

### Step 4: Assign step.sampling_state = original_state

```python
step.sampling_state = original_state
```

### Step 5: Assign values2 = step.rng.random(...)

```python
values2 = step.rng.random(100)
```

**Verification:**
```python
assert np.array_equal(values1, values2, equal_nan=True)
```


## Complete Example

```python
# Setup
# Fixtures: step

# Workflow
original_state = step.sampling_state
values1 = step.rng.random(100)
final_state = step.sampling_state
assert not equal_sampling_states(original_state, final_state)
step.sampling_state = original_state
values2 = step.rng.random(100)
assert np.array_equal(values1, values2, equal_nan=True)
assert equal_sampling_states(step.sampling_state, final_state)
```

## Next Steps


---

*Source: test_state.py:148 | Complexity: Intermediate | Last updated: 2026-05-18*