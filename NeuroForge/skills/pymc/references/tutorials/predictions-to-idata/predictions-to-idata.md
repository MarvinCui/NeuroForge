# How To: Predictions To Idata

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that we can add predictions to a previously-existing xarray.DataTree.

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

### Step 1: 'Test that we can add predictions to a previously-existing xarray.DataTree.'

```python
'Test that we can add predictions to a previously-existing xarray.DataTree.'
```

**Verification:**
```python
assert not fails
```

### Step 2: Assign test_dict = value

```python
test_dict = {'posterior': ['mu', 'tau', 'eta', 'theta'], 'sample_stats': ['diverging', 'lp'], 'predictions': ['obs'], 'prior': ['mu', 'tau', 'eta', 'theta'], 'observed_data': ['obs']}
```

**Verification:**
```python
assert len(ivalues['chain']) == inference_data.posterior.sizes['chain']
```

### Step 3: Assign unknown = self.get_predictions_inference_data(...)

```python
inference_data, _ = self.get_predictions_inference_data(data, eight_schools_params, False)
```

**Verification:**
```python
assert not fails
```

### Step 4: Assign fails = check_multiple_attrs(...)

```python
fails = check_multiple_attrs(test_dict, inference_data)
```

**Verification:**
```python
assert len(ivalues['chain']) == inference_data.posterior.sizes['chain']
```

### Step 5: Assign unknown = self.get_predictions_inference_data(...)

```python
inference_data, posterior_predictive = self.get_predictions_inference_data(data, eight_schools_params, True)
```

### Step 6: Assign fails = check_multiple_attrs(...)

```python
fails = check_multiple_attrs(test_dict, inference_data)
```

**Verification:**
```python
assert not fails
```


## Complete Example

```python
# Setup
# Fixtures: data, eight_schools_params

# Workflow
'Test that we can add predictions to a previously-existing xarray.DataTree.'
test_dict = {'posterior': ['mu', 'tau', 'eta', 'theta'], 'sample_stats': ['diverging', 'lp'], 'predictions': ['obs'], 'prior': ['mu', 'tau', 'eta', 'theta'], 'observed_data': ['obs']}
inference_data, _ = self.get_predictions_inference_data(data, eight_schools_params, False)
fails = check_multiple_attrs(test_dict, inference_data)
assert not fails
for key, ivalues in inference_data.predictions.items():
    assert len(ivalues['chain']) == inference_data.posterior.sizes['chain']
inference_data, posterior_predictive = self.get_predictions_inference_data(data, eight_schools_params, True)
fails = check_multiple_attrs(test_dict, inference_data)
assert not fails
for key, ivalues in inference_data.predictions.items():
    assert len(ivalues['chain']) == inference_data.posterior.sizes['chain']
```

## Next Steps


---

*Source: test_arviz.py:169 | Complexity: Intermediate | Last updated: 2026-05-18*