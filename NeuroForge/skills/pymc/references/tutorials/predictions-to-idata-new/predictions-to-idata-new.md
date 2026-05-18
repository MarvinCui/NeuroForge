# How To: Predictions To Idata New

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test predictions to idata new

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `re`
- `warnings`
- `numpy`
- `pytest`
- `xarray`
- `arviz_base.testing`
- `numpy`
- `pytensor.tensor.subtensor`
- `pymc`
- `pymc.backends.arviz`
- `pymc.exceptions`

**Setup Required:**
```python
# Fixtures: data, eight_schools_params
```

## Step-by-Step Guide

### Step 1: Assign unknown = self.make_predictions_inference_data(...)

```python
inference_data, posterior_predictive = self.make_predictions_inference_data(data, eight_schools_params)
```

**Verification:**
```python
assert not fails
```

### Step 2: Assign test_dict = value

```python
test_dict = {'posterior': ['mu', 'tau', 'eta', 'theta'], 'predictions': ['obs'], '~observed_data': ''}
```

**Verification:**
```python
assert len(ivalues['chain']) == 2 and len(ivalues['draw']) == 500
```

### Step 3: Assign fails = check_multiple_attrs(...)

```python
fails = check_multiple_attrs(test_dict, inference_data)
```

**Verification:**
```python
assert not fails
```

### Step 4: Assign ivalues = value

```python
ivalues = inference_data.predictions[key]
```

**Verification:**
```python
assert len(ivalues['chain']) == 2 and len(ivalues['draw']) == 500
```


## Complete Example

```python
# Setup
# Fixtures: data, eight_schools_params

# Workflow
inference_data, posterior_predictive = self.make_predictions_inference_data(data, eight_schools_params)
test_dict = {'posterior': ['mu', 'tau', 'eta', 'theta'], 'predictions': ['obs'], '~observed_data': ''}
fails = check_multiple_attrs(test_dict, inference_data)
assert not fails
for key, values in posterior_predictive.items():
    ivalues = inference_data.predictions[key]
    assert len(ivalues['chain']) == 2 and len(ivalues['draw']) == 500
```

## Next Steps


---

*Source: test_arviz.py:199 | Complexity: Intermediate | Last updated: 2026-05-18*