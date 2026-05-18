# How To: Choose Chains

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test choose chains

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `pymc`
- `pymc.backends`
- `pymc.backends.base`

**Setup Required:**
```python
# Fixtures: n_points, tune, expected_length, expected_n_traces
```

## Step-by-Step Guide

### Step 1: Assign trace_0 = np.arange(...)

```python
trace_0 = np.arange(n_points[0])
```

**Verification:**
```python
assert length == expected_length
```

### Step 2: Assign trace_1 = np.arange(...)

```python
trace_1 = np.arange(n_points[1])
```

**Verification:**
```python
assert expected_n_traces == len(traces)
```

### Step 3: Assign trace_2 = np.arange(...)

```python
trace_2 = np.arange(n_points[2])
```

### Step 4: Assign unknown = _choose_chains(...)

```python
traces, length = _choose_chains([trace_0, trace_1, trace_2], tune=tune)
```

**Verification:**
```python
assert length == expected_length
```


## Complete Example

```python
# Setup
# Fixtures: n_points, tune, expected_length, expected_n_traces

# Workflow
trace_0 = np.arange(n_points[0])
trace_1 = np.arange(n_points[1])
trace_2 = np.arange(n_points[2])
traces, length = _choose_chains([trace_0, trace_1, trace_2], tune=tune)
assert length == expected_length
assert expected_n_traces == len(traces)
```

## Next Steps


---

*Source: test_base.py:30 | Complexity: Intermediate | Last updated: 2026-05-18*