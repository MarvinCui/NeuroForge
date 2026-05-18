# How To: Uniform And Thresholding

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
assert_allclose(stc1._data, np.array([[0, -1.0]]))
```

### Step 2: Assign src = read_source_spaces(...)

```python
src = read_source_spaces(src_fname)
```

**Verification:**
```python
assert_allclose(stc2._data, np.array([[0, -1.0]]))
```

### Step 3: Assign vert = value

```python
vert = [src[0]['vertno'][0:1], []]
```

**Verification:**
```python
assert_allclose(threshold, metrics._check_threshold(threshold))
```

### Step 4: Assign data = np.array(...)

```python
data = np.array([[0.8, -1.0]])
```

### Step 5: Assign stc_true = SourceEstimate(...)

```python
stc_true = SourceEstimate(data, vert, 0, 0.002, subject='sample')
```

### Step 6: Assign stc_bad = SourceEstimate(...)

```python
stc_bad = SourceEstimate(data, vert, 0, 0.002, subject='sample')
```

### Step 7: Assign stc_bad.vertices = value

```python
stc_bad.vertices = [stc_bad.vertices[0]]
```

### Step 8: Assign threshold = 0.9

```python
threshold = 0.9
```

### Step 9: Assign unknown = metrics._thresholding(...)

```python
stc1, stc2 = metrics._thresholding(stc_true, stc_true, threshold)
```

### Step 10: Call assert_allclose()

```python
assert_allclose(stc1._data, np.array([[0, -1.0]]))
```

### Step 11: Call assert_allclose()

```python
assert_allclose(stc2._data, np.array([[0, -1.0]]))
```

### Step 12: Call assert_allclose()

```python
assert_allclose(threshold, metrics._check_threshold(threshold))
```

### Step 13: Assign threshold = '90'

```python
threshold = '90'
```

### Step 14: Call metrics._uniform_stc()

```python
metrics._uniform_stc(stc_true, stc_bad)
```

### Step 15: Call metrics._check_threshold()

```python
metrics._check_threshold(threshold)
```


## Complete Example

```python
# Workflow
'Test simulation metrics.'
src = read_source_spaces(src_fname)
vert = [src[0]['vertno'][0:1], []]
data = np.array([[0.8, -1.0]])
stc_true = SourceEstimate(data, vert, 0, 0.002, subject='sample')
stc_bad = SourceEstimate(data, vert, 0, 0.002, subject='sample')
stc_bad.vertices = [stc_bad.vertices[0]]
with pytest.raises(ValueError, match='same number of vertices'):
    metrics._uniform_stc(stc_true, stc_bad)
threshold = 0.9
stc1, stc2 = metrics._thresholding(stc_true, stc_true, threshold)
assert_allclose(stc1._data, np.array([[0, -1.0]]))
assert_allclose(stc2._data, np.array([[0, -1.0]]))
assert_allclose(threshold, metrics._check_threshold(threshold))
threshold = '90'
with pytest.raises(ValueError, match='Threshold if a str.*'):
    metrics._check_threshold(threshold)
```

## Next Steps


---

*Source: test_metrics.py:30 | Complexity: Advanced | Last updated: 2026-05-18*