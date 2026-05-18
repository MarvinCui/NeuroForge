# How To: Compute Microstructure Uncertainty Ambiguity Different Ranges

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that prior_range correctly normalizes uncertainty/ambiguity.

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.reconst.force`


## Step-by-Step Guide

### Step 1: 'Test that prior_range correctly normalizes uncertainty/ambiguity.'

```python
'Test that prior_range correctly normalizes uncertainty/ambiguity.'
```

**Verification:**
```python
assert unc_large[0] < unc_small[0]
```

### Step 2: Assign vals = np.array(...)

```python
vals = np.array([[0.0, 0.25, 0.5, 0.75, 1.0]], dtype=np.float32)
```

**Verification:**
```python
assert amb_large[0] < amb_small[0]
```

### Step 3: Assign weights = np.array(...)

```python
weights = np.array([[0.2, 0.2, 0.2, 0.2, 0.2]], dtype=np.float32)
```

### Step 4: Assign unknown = compute_microstructure_uncertainty_ambiguity(...)

```python
unc_small, amb_small = compute_microstructure_uncertainty_ambiguity(vals, weights, prior_range=1.0)
```

### Step 5: Assign unknown = compute_microstructure_uncertainty_ambiguity(...)

```python
unc_large, amb_large = compute_microstructure_uncertainty_ambiguity(vals, weights, prior_range=10.0)
```

**Verification:**
```python
assert unc_large[0] < unc_small[0]
```


## Complete Example

```python
# Workflow
'Test that prior_range correctly normalizes uncertainty/ambiguity.'
vals = np.array([[0.0, 0.25, 0.5, 0.75, 1.0]], dtype=np.float32)
weights = np.array([[0.2, 0.2, 0.2, 0.2, 0.2]], dtype=np.float32)
unc_small, amb_small = compute_microstructure_uncertainty_ambiguity(vals, weights, prior_range=1.0)
unc_large, amb_large = compute_microstructure_uncertainty_ambiguity(vals, weights, prior_range=10.0)
assert unc_large[0] < unc_small[0]
assert amb_large[0] < amb_small[0]
```

## Next Steps


---

*Source: test_force.py:220 | Complexity: Intermediate | Last updated: 2026-05-18*