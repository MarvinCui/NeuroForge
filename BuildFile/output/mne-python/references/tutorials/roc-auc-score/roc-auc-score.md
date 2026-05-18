# How To: Roc Auc Score

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
assert_allclose(score, 0.75)
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('sklearn')
```

### Step 3: Assign src = read_source_spaces(...)

```python
src = read_source_spaces(src_fname)
```

### Step 4: Assign vert1 = value

```python
vert1 = [src[0]['vertno'][0:4], []]
```

### Step 5: Assign vert2 = value

```python
vert2 = [src[0]['vertno'][0:4], []]
```

### Step 6: Assign data1 = value

```python
data1 = np.array([[0.0, 0.0, 1, 1]]).T
```

### Step 7: Assign data2 = value

```python
data2 = np.array([[0.1, -0.4, 0.35, 0.8]]).T
```

### Step 8: Assign stc_true = SourceEstimate(...)

```python
stc_true = SourceEstimate(data1, vert1, 0, 0.002, subject='sample')
```

### Step 9: Assign stc_est = SourceEstimate(...)

```python
stc_est = SourceEstimate(data2, vert2, 0, 0.002, subject='sample')
```

### Step 10: Assign score = roc_auc_score(...)

```python
score = roc_auc_score(stc_true, stc_est, per_sample=False)
```

### Step 11: Call assert_allclose()

```python
assert_allclose(score, 0.75)
```


## Complete Example

```python
# Workflow
'Test simulation metrics.'
pytest.importorskip('sklearn')
src = read_source_spaces(src_fname)
vert1 = [src[0]['vertno'][0:4], []]
vert2 = [src[0]['vertno'][0:4], []]
data1 = np.array([[0.0, 0.0, 1, 1]]).T
data2 = np.array([[0.1, -0.4, 0.35, 0.8]]).T
stc_true = SourceEstimate(data1, vert1, 0, 0.002, subject='sample')
stc_est = SourceEstimate(data2, vert2, 0, 0.002, subject='sample')
score = roc_auc_score(stc_true, stc_est, per_sample=False)
assert_allclose(score, 0.75)
```

## Next Steps


---

*Source: test_metrics.py:185 | Complexity: Advanced | Last updated: 2026-05-18*