# How To: Cosine Score

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
assert_allclose(E_per_sample1, np.zeros(2))
```

### Step 2: Assign src = read_source_spaces(...)

```python
src = read_source_spaces(src_fname)
```

**Verification:**
```python
assert_allclose(E_unique1, 0.0, atol=1e-08)
```

### Step 3: Assign vert1 = value

```python
vert1 = [src[0]['vertno'][0:1], []]
```

**Verification:**
```python
assert_allclose(E_per_sample2, np.ones(2))
```

### Step 4: Assign vert2 = value

```python
vert2 = [src[0]['vertno'][1:2], []]
```

**Verification:**
```python
assert_allclose(E_unique2, 1.0, atol=1e-08)
```

### Step 5: Assign data1 = np.ones(...)

```python
data1 = np.ones((1, 2))
```

### Step 6: Assign data2 = data1.copy(...)

```python
data2 = data1.copy()
```

### Step 7: Assign stc_true = SourceEstimate(...)

```python
stc_true = SourceEstimate(data1, vert1, 0, 0.002, subject='sample')
```

### Step 8: Assign stc_est1 = SourceEstimate(...)

```python
stc_est1 = SourceEstimate(data2, vert2, 0, 0.002, subject='sample')
```

### Step 9: Assign stc_est2 = SourceEstimate(...)

```python
stc_est2 = SourceEstimate(data2, vert1, 0, 0.002, subject='sample')
```

### Step 10: Assign E_per_sample1 = cosine_score(...)

```python
E_per_sample1 = cosine_score(stc_true, stc_est1)
```

### Step 11: Assign E_unique1 = cosine_score(...)

```python
E_unique1 = cosine_score(stc_true, stc_est1, per_sample=False)
```

### Step 12: Assign E_per_sample2 = cosine_score(...)

```python
E_per_sample2 = cosine_score(stc_true, stc_est2)
```

### Step 13: Assign E_unique2 = cosine_score(...)

```python
E_unique2 = cosine_score(stc_true, stc_est2, per_sample=False)
```

### Step 14: Call assert_allclose()

```python
assert_allclose(E_per_sample1, np.zeros(2))
```

### Step 15: Call assert_allclose()

```python
assert_allclose(E_unique1, 0.0, atol=1e-08)
```

### Step 16: Call assert_allclose()

```python
assert_allclose(E_per_sample2, np.ones(2))
```

### Step 17: Call assert_allclose()

```python
assert_allclose(E_unique2, 1.0, atol=1e-08)
```


## Complete Example

```python
# Workflow
'Test simulation metrics.'
src = read_source_spaces(src_fname)
vert1 = [src[0]['vertno'][0:1], []]
vert2 = [src[0]['vertno'][1:2], []]
data1 = np.ones((1, 2))
data2 = data1.copy()
stc_true = SourceEstimate(data1, vert1, 0, 0.002, subject='sample')
stc_est1 = SourceEstimate(data2, vert2, 0, 0.002, subject='sample')
stc_est2 = SourceEstimate(data2, vert1, 0, 0.002, subject='sample')
E_per_sample1 = cosine_score(stc_true, stc_est1)
E_unique1 = cosine_score(stc_true, stc_est1, per_sample=False)
E_per_sample2 = cosine_score(stc_true, stc_est2)
E_unique2 = cosine_score(stc_true, stc_est2, per_sample=False)
assert_allclose(E_per_sample1, np.zeros(2))
assert_allclose(E_unique1, 0.0, atol=1e-08)
assert_allclose(E_per_sample2, np.ones(2))
assert_allclose(E_unique2, 1.0, atol=1e-08)
```

## Next Steps


---

*Source: test_metrics.py:53 | Complexity: Advanced | Last updated: 2026-05-18*