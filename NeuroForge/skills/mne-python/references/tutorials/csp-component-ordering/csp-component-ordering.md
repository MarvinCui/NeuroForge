# How To: Csp Component Ordering

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that CSP component ordering works as expected.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `sklearn.linear_model`
- `sklearn.model_selection`
- `sklearn.pipeline`
- `sklearn.svm`
- `sklearn.utils.estimator_checks`
- `mne`
- `mne.decoding`
- `mne.decoding.csp`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test that CSP component ordering works as expected.'

```python
'Test that CSP component ordering works as expected.'
```

**Verification:**
```python
assert_array_almost_equal(p_alt, p_mut[[2, 0, 3, 1]])
```

### Step 2: Assign unknown = deterministic_toy_data(...)

```python
x, y = deterministic_toy_data(['class_a', 'class_b'])
```

### Step 3: Assign csp = CSP(...)

```python
csp = CSP(component_order='invalid')
```

### Step 4: Assign csp = CSP(...)

```python
csp = CSP(component_order='alternate')
```

### Step 5: Assign p_alt = value

```python
p_alt = CSP(component_order='alternate').fit(x, y).patterns_
```

### Step 6: Assign p_mut = value

```python
p_mut = CSP(component_order='mutual_info').fit(x, y).patterns_
```

### Step 7: Call assert_array_almost_equal()

```python
assert_array_almost_equal(p_alt, p_mut[[2, 0, 3, 1]])
```

### Step 8: Call csp.fit()

```python
csp.fit(x, y)
```

### Step 9: Call csp.fit()

```python
csp.fit(np.zeros((3, 0, 0)), ['a', 'b', 'c'])
```


## Complete Example

```python
# Workflow
'Test that CSP component ordering works as expected.'
x, y = deterministic_toy_data(['class_a', 'class_b'])
csp = CSP(component_order='invalid')
with pytest.raises(ValueError, match='Invalid value'):
    csp.fit(x, y)
csp = CSP(component_order='alternate')
with pytest.raises(ValueError):
    csp.fit(np.zeros((3, 0, 0)), ['a', 'b', 'c'])
p_alt = CSP(component_order='alternate').fit(x, y).patterns_
p_mut = CSP(component_order='mutual_info').fit(x, y).patterns_
assert_array_almost_equal(p_alt, p_mut[[2, 0, 3, 1]])
```

## Next Steps


---

*Source: test_csp.py:475 | Complexity: Advanced | Last updated: 2026-05-18*