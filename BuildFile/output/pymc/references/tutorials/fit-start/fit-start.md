# How To: Fit Start

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test fit start

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `io`
- `operator`
- `warnings`
- `cloudpickle`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `pymc`
- `pymc.variational.opvi`
- `pymc.model.transform.basic`
- `pymc.pytensorf`
- `pymc.variational.inference`
- `pymc.variational.opvi`
- `tests`

**Setup Required:**
```python
# Fixtures: inference_spec, simple_model
```

## Step-by-Step Guide

### Step 1: Assign mu_init = 17

```python
mu_init = 17
```

### Step 2: Assign mu_sigma_init = 13

```python
mu_sigma_init = 13
```

### Step 3: Assign kw = value

```python
kw = {'start': {'mu': mu_init}}
```

### Step 4: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(np.mean(trace.posterior['mu']), mu_init, rtol=0.05)
```

### Step 5: Call kw.update()

```python
kw.update({'start_sigma': {'mu': mu_sigma_init}})
```

### Step 6: Assign inference = inference_spec(...)

```python
inference = inference_spec(**kw)
```

### Step 7: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(np.std(trace.posterior['mu']), mu_sigma_init, rtol=0.05)
```

### Step 8: Assign trace = inference.fit.sample(...)

```python
trace = inference.fit(n=0).sample(10000)
```

### Step 9: Call pytest.skip()

```python
pytest.skip(str(e))
```

### Step 10: Assign has_start_sigma = True

```python
has_start_sigma = True
```

### Step 11: Assign has_start_sigma = False

```python
has_start_sigma = False
```


## Complete Example

```python
# Setup
# Fixtures: inference_spec, simple_model

# Workflow
mu_init = 17
mu_sigma_init = 13
with simple_model:
    if type(inference_spec()) is ASVGD:
        return
    elif type(inference_spec()) is ADVI:
        has_start_sigma = True
    else:
        has_start_sigma = False
kw = {'start': {'mu': mu_init}}
if has_start_sigma:
    kw.update({'start_sigma': {'mu': mu_sigma_init}})
with simple_model:
    inference = inference_spec(**kw)
try:
    with simple_model:
        trace = inference.fit(n=0).sample(10000)
except NotImplementedInference as e:
    pytest.skip(str(e))
np.testing.assert_allclose(np.mean(trace.posterior['mu']), mu_init, rtol=0.05)
if has_start_sigma:
    np.testing.assert_allclose(np.std(trace.posterior['mu']), mu_sigma_init, rtol=0.05)
```

## Next Steps


---

*Source: test_inference.py:189 | Complexity: Advanced | Last updated: 2026-05-18*