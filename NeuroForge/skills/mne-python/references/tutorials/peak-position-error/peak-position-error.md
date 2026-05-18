# How To: Peak Position Error

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
assert_allclose(score, norm(r_true - r_mean))
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

### Step 9: Assign r_mean = value

```python
r_mean = 0.5 * (src[0]['rr'][vert2[0][0]] + src[0]['rr'][vert2[0][1]])
```

### Step 10: Assign r_true = value

```python
r_true = src[0]['rr'][vert2[0][0]]
```

### Step 11: Assign score = peak_position_error(...)

```python
score = peak_position_error(stc_true, stc_est, src, per_sample=False)
```

### Step 12: Call assert_allclose()

```python
assert_allclose(score, norm(r_true - r_mean))
```

### Step 13: Assign data2 = value

```python
data2 = np.array([[0, 0.0]]).T
```

### Step 14: Assign stc_est = SourceEstimate(...)

```python
stc_est = SourceEstimate(data2, vert2, 0, 0.002, subject='sample')
```

### Step 15: Assign score = peak_position_error(...)

```python
score = peak_position_error(stc_true, stc_est, src, per_sample=False)
```

### Step 16: Call assert_allclose()

```python
assert_allclose(score, np.inf)
```

### Step 17: Call peak_position_error()

```python
peak_position_error(stc_est, stc_est, src)
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
r_mean = 0.5 * (src[0]['rr'][vert2[0][0]] + src[0]['rr'][vert2[0][1]])
r_true = src[0]['rr'][vert2[0][0]]
score = peak_position_error(stc_true, stc_est, src, per_sample=False)
assert_allclose(score, norm(r_true - r_mean))
with pytest.raises(ValueError, match='must contain only one dipole'):
    peak_position_error(stc_est, stc_est, src)
data2 = np.array([[0, 0.0]]).T
stc_est = SourceEstimate(data2, vert2, 0, 0.002, subject='sample')
score = peak_position_error(stc_true, stc_est, src, per_sample=False)
assert_allclose(score, np.inf)
```

## Next Steps


---

*Source: test_metrics.py:201 | Complexity: Advanced | Last updated: 2026-05-18*