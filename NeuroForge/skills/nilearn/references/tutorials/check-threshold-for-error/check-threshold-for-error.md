# How To: Check Threshold For Error

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Tests nilearn._utils.param_validation.check_threshold for errors.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `scipy.stats`
- `nilearn._utils.extmath`
- `nilearn._utils.param_validation`

**Setup Required:**
```python
# Fixtures: matrix
```

## Step-by-Step Guide

### Step 1: 'Tests nilearn._utils.param_validation.check_threshold for errors.'

```python
'Tests nilearn._utils.param_validation.check_threshold for errors.'
```

### Step 2: Assign name = 'threshold'

```python
name = 'threshold'
```

### Step 3: Assign wrong_thresholds = value

```python
wrong_thresholds = ['0.1', '10', '10.2.3%', 'asdf%']
```

### Step 4: Assign threshold = object(...)

```python
threshold = object()
```

### Step 5: Assign two_sided = True

```python
two_sided = True
```

### Step 6: Assign thresholds = value

```python
thresholds = [-10, '-10%']
```

### Step 7: Call check_threshold()

```python
check_threshold('-10%', matrix, fast_abs_percentile, name, two_sided=False)
```

### Step 8: Call check_threshold()

```python
check_threshold(threshold, matrix, fast_abs_percentile, name, two_sided)
```

### Step 9: Call check_threshold()

```python
check_threshold(wrong_threshold, matrix, fast_abs_percentile, name, two_sided)
```

### Step 10: Call check_threshold()

```python
check_threshold(wrong_threshold, matrix, fast_abs_percentile, name, two_sided)
```


## Complete Example

```python
# Setup
# Fixtures: matrix

# Workflow
'Tests nilearn._utils.param_validation.check_threshold for errors.'
name = 'threshold'
wrong_thresholds = ['0.1', '10', '10.2.3%', 'asdf%']
for wrong_threshold in wrong_thresholds:
    for two_sided in [True, False]:
        with pytest.raises(ValueError, match=f'{name}.+should be a number followed'):
            check_threshold(wrong_threshold, matrix, fast_abs_percentile, name, two_sided)
threshold = object()
for two_sided in [True, False]:
    with pytest.raises(TypeError, match=f'{name}.+should be either a number or a string'):
        check_threshold(threshold, matrix, fast_abs_percentile, name, two_sided)
two_sided = True
thresholds = [-10, '-10%']
for wrong_threshold in thresholds:
    with pytest.raises(ValueError, match=f'{name}.+should not be a negative'):
        check_threshold(wrong_threshold, matrix, fast_abs_percentile, name, two_sided)
with pytest.raises(ValueError, match=f'{name}.+should not be a negative'):
    check_threshold('-10%', matrix, fast_abs_percentile, name, two_sided=False)
```

## Next Steps


---

*Source: test_param_validation.py:121 | Complexity: Advanced | Last updated: 2026-05-18*