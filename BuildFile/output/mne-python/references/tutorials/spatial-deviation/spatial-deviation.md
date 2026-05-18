# How To: Spatial Deviation

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test simulation metrics.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy.linalg`
- `mne`
- `mne.datasets`
- `mne.simulation`
- `mne.simulation.metrics`
- `sklearn.exceptions`


## Step-by-Step Guide

### Step 1: 'Test simulation metrics.'

```python
'Test simulation metrics.'
```

**Verification:**
```python
assert_allclose(score, std)
```

### Step 2: Assign src = read_source_spaces(...)

```python
src = read_source_spaces(src_fname)
```

**Verification:**
```python
assert_allclose(score, np.inf)
```

### Step 3: Assign vert1 = value

```python
vert1 = [src[0]['vertno'][0:1], []]
```

### Step 4: Assign vert2 = value

```python
vert2 = [src[0]['vertno'][0:2], []]
```

### Step 5: Assign data1 = np.array(...)

```python
data1 = np.array([[1]])
```

### Step 6: Assign data2 = value

```python
data2 = np.array([[1, 1.0]]).T
```

### Step 7: Assign stc_true = SourceEstimate(...)

```python
stc_true = SourceEstimate(data1, vert1, 0, 0.002, subject='sample')
```

### Step 8: Assign stc_est = SourceEstimate(...)

```python
stc_est = SourceEstimate(data2, vert2, 0, 0.002, subject='sample')
```

### Step 9: Assign std = np.sqrt(...)

```python
std = np.sqrt(0.5 * (0 + norm(src[0]['rr'][vert2[0][1]] - src[0]['rr'][vert2[0][0]]) ** 2))
```

### Step 10: Assign score = spatial_deviation_error(...)

```python
score = spatial_deviation_error(stc_true, stc_est, src, per_sample=False)
```

### Step 11: Call assert_allclose()

```python
assert_allclose(score, std)
```

### Step 12: Assign data2 = value

```python
data2 = np.array([[0, 0.0]]).T
```

### Step 13: Assign stc_est = SourceEstimate(...)

```python
stc_est = SourceEstimate(data2, vert2, 0, 0.002, subject='sample')
```

### Step 14: Assign score = spatial_deviation_error(...)

```python
score = spatial_deviation_error(stc_true, stc_est, src, per_sample=False)
```

### Step 15: Call assert_allclose()

```python
assert_allclose(score, np.inf)
```


## Complete Example

```python
# Workflow
'Test simulation metrics.'
src = read_source_spaces(src_fname)
vert1 = [src[0]['vertno'][0:1], []]
vert2 = [src[0]['vertno'][0:2], []]
data1 = np.array([[1]])
data2 = np.array([[1, 1.0]]).T
stc_true = SourceEstimate(data1, vert1, 0, 0.002, subject='sample')
stc_est = SourceEstimate(data2, vert2, 0, 0.002, subject='sample')
std = np.sqrt(0.5 * (0 + norm(src[0]['rr'][vert2[0][1]] - src[0]['rr'][vert2[0][0]]) ** 2))
score = spatial_deviation_error(stc_true, stc_est, src, per_sample=False)
assert_allclose(score, std)
data2 = np.array([[0, 0.0]]).T
stc_est = SourceEstimate(data2, vert2, 0, 0.002, subject='sample')
score = spatial_deviation_error(stc_true, stc_est, src, per_sample=False)
assert_allclose(score, np.inf)
```

## Next Steps


---

*Source: test_metrics.py:225 | Complexity: Advanced | Last updated: 2026-05-18*