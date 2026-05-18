# How To: Precision Score

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
assert_allclose(E_unique1, 0.5)
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('sklearn')
```

**Verification:**
```python
assert_allclose(E_unique2, 1.0)
```

### Step 3: Assign src = read_source_spaces(...)

```python
src = read_source_spaces(src_fname)
```

**Verification:**
```python
assert_allclose(E_per_sample1, [0.0, 1.0])
```

### Step 4: Assign vert1 = value

```python
vert1 = [src[0]['vertno'][0:2], []]
```

**Verification:**
```python
assert_allclose(E_per_sample2, [1.0, 1.0])
```

### Step 5: Assign vert2 = value

```python
vert2 = [src[0]['vertno'][1:3], []]
```

### Step 6: Assign vert3 = value

```python
vert3 = [src[0]['vertno'][0:1], []]
```

### Step 7: Assign data1 = np.ones(...)

```python
data1 = np.ones((2, 2))
```

### Step 8: Assign data2 = np.ones(...)

```python
data2 = np.ones((2, 2))
```

### Step 9: Assign data3 = np.array(...)

```python
data3 = np.array([[0.8, 1]])
```

### Step 10: Assign stc_true = SourceEstimate(...)

```python
stc_true = SourceEstimate(data1, vert1, 0, 0.002, subject='sample')
```

### Step 11: Assign stc_est1 = SourceEstimate(...)

```python
stc_est1 = SourceEstimate(data2, vert2, 0, 0.002, subject='sample')
```

### Step 12: Assign stc_est2 = SourceEstimate(...)

```python
stc_est2 = SourceEstimate(data3, vert3, 0, 0.002, subject='sample')
```

### Step 13: Assign E_unique1 = precision_score(...)

```python
E_unique1 = precision_score(stc_true, stc_est1, per_sample=False)
```

### Step 14: Assign E_unique2 = precision_score(...)

```python
E_unique2 = precision_score(stc_true, stc_est2, per_sample=False)
```

### Step 15: Assign E_per_sample2 = precision_score(...)

```python
E_per_sample2 = precision_score(stc_true, stc_est2, threshold='70%')
```

### Step 16: Call assert_allclose()

```python
assert_allclose(E_unique1, 0.5)
```

### Step 17: Call assert_allclose()

```python
assert_allclose(E_unique2, 1.0)
```

### Step 18: Call assert_allclose()

```python
assert_allclose(E_per_sample1, [0.0, 1.0])
```

### Step 19: Call assert_allclose()

```python
assert_allclose(E_per_sample2, [1.0, 1.0])
```

### Step 20: Assign E_per_sample1 = precision_score(...)

```python
E_per_sample1 = precision_score(stc_true, stc_est2)
```

### Step 21: Call precision_score()

```python
precision_score(stc_true, stc_est2, threshold=2)
```


## Complete Example

```python
# Workflow
'Test simulation metrics.'
pytest.importorskip('sklearn')
from sklearn.exceptions import UndefinedMetricWarning
src = read_source_spaces(src_fname)
vert1 = [src[0]['vertno'][0:2], []]
vert2 = [src[0]['vertno'][1:3], []]
vert3 = [src[0]['vertno'][0:1], []]
data1 = np.ones((2, 2))
data2 = np.ones((2, 2))
data3 = np.array([[0.8, 1]])
stc_true = SourceEstimate(data1, vert1, 0, 0.002, subject='sample')
stc_est1 = SourceEstimate(data2, vert2, 0, 0.002, subject='sample')
stc_est2 = SourceEstimate(data3, vert3, 0, 0.002, subject='sample')
E_unique1 = precision_score(stc_true, stc_est1, per_sample=False)
E_unique2 = precision_score(stc_true, stc_est2, per_sample=False)
with pytest.warns(UndefinedMetricWarning, match='no predicted samples'):
    E_per_sample1 = precision_score(stc_true, stc_est2)
E_per_sample2 = precision_score(stc_true, stc_est2, threshold='70%')
with pytest.raises(ValueError, match='0 and 1'):
    precision_score(stc_true, stc_est2, threshold=2)
assert_allclose(E_unique1, 0.5)
assert_allclose(E_unique2, 1.0)
assert_allclose(E_per_sample1, [0.0, 1.0])
assert_allclose(E_per_sample2, [1.0, 1.0])
```

## Next Steps


---

*Source: test_metrics.py:99 | Complexity: Advanced | Last updated: 2026-05-18*