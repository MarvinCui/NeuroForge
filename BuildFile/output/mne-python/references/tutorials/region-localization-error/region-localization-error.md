# How To: Region Localization Error

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
assert_allclose(E_per_sample1, [np.inf, dist])
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('sklearn')
```

**Verification:**
```python
assert_allclose(E_per_sample2, [dist, dist])
```

### Step 3: Assign src = read_source_spaces(...)

```python
src = read_source_spaces(src_fname)
```

**Verification:**
```python
assert_allclose(E_unique, dist)
```

### Step 4: Assign vert1 = value

```python
vert1 = [src[0]['vertno'][0:1], []]
```

### Step 5: Assign vert2 = value

```python
vert2 = [src[0]['vertno'][1:2], []]
```

### Step 6: Assign dist = norm(...)

```python
dist = norm(src[0]['rr'][vert1[0]] - src[0]['rr'][vert2[0]])
```

### Step 7: Assign data1 = np.ones(...)

```python
data1 = np.ones((1, 2))
```

### Step 8: Assign data2 = np.array(...)

```python
data2 = np.array([[0.8, 1]])
```

### Step 9: Assign stc_true = SourceEstimate(...)

```python
stc_true = SourceEstimate(data1, vert1, 0, 0.002, subject='sample')
```

### Step 10: Assign stc_est1 = SourceEstimate(...)

```python
stc_est1 = SourceEstimate(data2, vert2, 0, 0.002, subject='sample')
```

### Step 11: Assign E_per_sample1 = region_localization_error(...)

```python
E_per_sample1 = region_localization_error(stc_true, stc_est1, src)
```

### Step 12: Assign E_per_sample2 = region_localization_error(...)

```python
E_per_sample2 = region_localization_error(stc_true, stc_est1, src, threshold='70%')
```

### Step 13: Assign E_unique = region_localization_error(...)

```python
E_unique = region_localization_error(stc_true, stc_est1, src, per_sample=False)
```

### Step 14: Call assert_allclose()

```python
assert_allclose(E_per_sample1, [np.inf, dist])
```

### Step 15: Call assert_allclose()

```python
assert_allclose(E_per_sample2, [dist, dist])
```

### Step 16: Call assert_allclose()

```python
assert_allclose(E_unique, dist)
```


## Complete Example

```python
# Workflow
'Test simulation metrics.'
pytest.importorskip('sklearn')
src = read_source_spaces(src_fname)
vert1 = [src[0]['vertno'][0:1], []]
vert2 = [src[0]['vertno'][1:2], []]
dist = norm(src[0]['rr'][vert1[0]] - src[0]['rr'][vert2[0]])
data1 = np.ones((1, 2))
data2 = np.array([[0.8, 1]])
stc_true = SourceEstimate(data1, vert1, 0, 0.002, subject='sample')
stc_est1 = SourceEstimate(data2, vert2, 0, 0.002, subject='sample')
E_per_sample1 = region_localization_error(stc_true, stc_est1, src)
E_per_sample2 = region_localization_error(stc_true, stc_est1, src, threshold='70%')
E_unique = region_localization_error(stc_true, stc_est1, src, per_sample=False)
assert_allclose(E_per_sample1, [np.inf, dist])
assert_allclose(E_per_sample2, [dist, dist])
assert_allclose(E_unique, dist)
```

## Next Steps


---

*Source: test_metrics.py:77 | Complexity: Advanced | Last updated: 2026-05-18*