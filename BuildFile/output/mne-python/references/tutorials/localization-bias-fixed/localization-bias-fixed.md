# How To: Localization Bias Fixed

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test inverse localization bias for fixed minimum-norm solvers.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `copy`
- `re`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `mne`
- `mne`
- `mne.channels`
- `mne.datasets`
- `mne.epochs`
- `mne.event`
- `mne.fixes`
- `mne.forward`
- `mne.io`
- `mne.label`
- `mne.minimum_norm`
- `mne.source_estimate`
- `mne.source_space._source_space`
- `mne.surface`
- `mne.time_frequency`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: bias_params_fixed, method, lower, upper, depth
```

## Step-by-Step Guide

### Step 1: 'Test inverse localization bias for fixed minimum-norm solvers.'

```python
'Test inverse localization bias for fixed minimum-norm solvers.'
```

**Verification:**
```python
assert lower <= perc <= upper, method
```

### Step 2: Assign unknown = bias_params_fixed

```python
evoked, fwd, noise_cov, _, want = bias_params_fixed
```

### Step 3: Assign fwd_use = convert_forward_solution(...)

```python
fwd_use = convert_forward_solution(fwd, force_fixed=False)
```

### Step 4: Assign inv_fixed = make_inverse_operator(...)

```python
inv_fixed = make_inverse_operator(evoked.info, fwd_use, noise_cov, loose=0.0, depth=depth)
```

### Step 5: Assign loc = np.abs(...)

```python
loc = np.abs(apply_inverse(evoked, inv_fixed, lambda2, method, verbose='debug').data)
```

### Step 6: Assign perc = value

```python
perc = (want == np.argmax(loc, axis=0)).mean() * 100
```

**Verification:**
```python
assert lower <= perc <= upper, method
```


## Complete Example

```python
# Setup
# Fixtures: bias_params_fixed, method, lower, upper, depth

# Workflow
'Test inverse localization bias for fixed minimum-norm solvers.'
evoked, fwd, noise_cov, _, want = bias_params_fixed
fwd_use = convert_forward_solution(fwd, force_fixed=False)
inv_fixed = make_inverse_operator(evoked.info, fwd_use, noise_cov, loose=0.0, depth=depth)
loc = np.abs(apply_inverse(evoked, inv_fixed, lambda2, method, verbose='debug').data)
perc = (want == np.argmax(loc, axis=0)).mean() * 100
assert lower <= perc <= upper, method
```

## Next Steps


---

*Source: test_inverse.py:419 | Complexity: Intermediate | Last updated: 2026-05-18*