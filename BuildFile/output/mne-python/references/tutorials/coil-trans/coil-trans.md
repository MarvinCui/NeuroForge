# How To: Coil Trans

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test loc<->coil_trans functions.

## Prerequisites

**Required Modules:**
- `json`
- `pickle`
- `string`
- `datetime`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne._fiff`
- `mne._fiff._digitization`
- `mne._fiff.constants`
- `mne._fiff.meas_info`
- `mne._fiff.proj`
- `mne._fiff.tag`
- `mne._fiff.write`
- `mne.channels`
- `mne.datasets`
- `mne.event`
- `mne.io`
- `mne.minimum_norm`
- `mne.transforms`
- `mne.utils`
- `mne.utils._bunch`


## Step-by-Step Guide

### Step 1: 'Test loc<->coil_trans functions.'

```python
'Test loc<->coil_trans functions.'
```

**Verification:**
```python
assert_allclose(_loc_to_coil_trans(_coil_trans_to_loc(x)), x)
```

### Step 2: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(0)
```

**Verification:**
```python
assert_allclose(_coil_trans_to_loc(_loc_to_coil_trans(x)), x)
```

### Step 3: Assign x = rng.randn(...)

```python
x = rng.randn(4, 4)
```

### Step 4: Assign unknown = value

```python
x[3] = [0, 0, 0, 1]
```

### Step 5: Call assert_allclose()

```python
assert_allclose(_loc_to_coil_trans(_coil_trans_to_loc(x)), x)
```

### Step 6: Assign x = rng.randn(...)

```python
x = rng.randn(12)
```

### Step 7: Call assert_allclose()

```python
assert_allclose(_coil_trans_to_loc(_loc_to_coil_trans(x)), x)
```


## Complete Example

```python
# Workflow
'Test loc<->coil_trans functions.'
rng = np.random.RandomState(0)
x = rng.randn(4, 4)
x[3] = [0, 0, 0, 1]
assert_allclose(_loc_to_coil_trans(_coil_trans_to_loc(x)), x)
x = rng.randn(12)
assert_allclose(_coil_trans_to_loc(_loc_to_coil_trans(x)), x)
```

## Next Steps


---

*Source: test_meas_info.py:136 | Complexity: Intermediate | Last updated: 2026-05-18*