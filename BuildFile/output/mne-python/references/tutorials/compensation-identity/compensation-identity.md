# How To: Compensation Identity

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test compensation identity.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.compensator`
- `mne.io`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test compensation identity.'

```python
'Test compensation identity.'
```

**Verification:**
```python
assert get_current_comp(raw.info) == 3
```

### Step 2: Assign raw = read_raw_fif(...)

```python
raw = read_raw_fif(ctf_comp_fname)
```

**Verification:**
```python
assert comp1.shape == (340, 340)
```

### Step 3: Assign comp1 = make_compensator(...)

```python
comp1 = make_compensator(raw.info, 3, 1, exclude_comp_chs=False)
```

**Verification:**
```python
assert comp2.shape == (311, 340)
```

### Step 4: Assign comp2 = make_compensator(...)

```python
comp2 = make_compensator(raw.info, 3, 1, exclude_comp_chs=True)
```

**Verification:**
```python
assert_allclose(np.dot(comp1, comp2), desired, atol=1e-12)
```

### Step 5: Assign desired = np.eye(...)

```python
desired = np.eye(340)
```

**Verification:**
```python
assert_allclose(np.dot(comp2, comp1), desired, atol=1e-12)
```

### Step 6: Assign comp1 = make_compensator(...)

```python
comp1 = make_compensator(raw.info, from_, to)
```

### Step 7: Assign comp2 = make_compensator(...)

```python
comp2 = make_compensator(raw.info, to, from_)
```

### Step 8: Call assert_allclose()

```python
assert_allclose(np.dot(comp1, comp2), desired, atol=1e-12)
```

### Step 9: Call assert_allclose()

```python
assert_allclose(np.dot(comp2, comp1), desired, atol=1e-12)
```


## Complete Example

```python
# Workflow
'Test compensation identity.'
raw = read_raw_fif(ctf_comp_fname)
assert get_current_comp(raw.info) == 3
comp1 = make_compensator(raw.info, 3, 1, exclude_comp_chs=False)
assert comp1.shape == (340, 340)
comp2 = make_compensator(raw.info, 3, 1, exclude_comp_chs=True)
assert comp2.shape == (311, 340)
desired = np.eye(340)
for from_ in range(3):
    for to in range(3):
        if from_ == to:
            continue
        comp1 = make_compensator(raw.info, from_, to)
        comp2 = make_compensator(raw.info, to, from_)
        assert_allclose(np.dot(comp1, comp2), desired, atol=1e-12)
        assert_allclose(np.dot(comp2, comp1), desired, atol=1e-12)
```

## Next Steps


---

*Source: test_compensator.py:20 | Complexity: Advanced | Last updated: 2026-05-18*