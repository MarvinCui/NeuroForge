# How To: Csp Pipeline

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test if CSP works in a pipeline.

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

### Step 1: 'Test if CSP works in a pipeline.'

```python
'Test if CSP works in a pipeline.'
```

**Verification:**
```python
assert pipe.get_params()['CSP__reg'] == 0.2
```

### Step 2: Assign csp = CSP(...)

```python
csp = CSP(reg=1, norm_trace=False)
```

### Step 3: Assign svc = SVC(...)

```python
svc = SVC()
```

### Step 4: Assign pipe = Pipeline(...)

```python
pipe = Pipeline([('CSP', csp), ('SVC', svc)])
```

### Step 5: Call pipe.set_params()

```python
pipe.set_params(CSP__reg=0.2)
```

**Verification:**
```python
assert pipe.get_params()['CSP__reg'] == 0.2
```


## Complete Example

```python
# Workflow
'Test if CSP works in a pipeline.'
csp = CSP(reg=1, norm_trace=False)
svc = SVC()
pipe = Pipeline([('CSP', csp), ('SVC', svc)])
pipe.set_params(CSP__reg=0.2)
assert pipe.get_params()['CSP__reg'] == 0.2
```

## Next Steps


---

*Source: test_csp.py:387 | Complexity: Intermediate | Last updated: 2026-05-18*