# How To: Blockwise Sigma Array Support

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that blockwise method supports different sigma input formats.

## Prerequisites

**Required Modules:**
- `time`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.denoise.denspeed`
- `dipy.denoise.nlmeans`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.utils.omp`


## Step-by-Step Guide

### Step 1: '\n    Test that blockwise method supports different sigma input formats.\n    '

```python
'\n    Test that blockwise method supports different sigma input formats.\n    '
```

**Verification:**
```python
assert result1.shape == S0.shape
```

### Step 2: Assign S0 = value

```python
S0 = 100 * np.ones((20, 20, 20), dtype='f8')
```

**Verification:**
```python
assert result2.shape == S0.shape
```

### Step 3: Assign result1 = nlmeans(...)

```python
result1 = nlmeans(S0, sigma=1.0, method='blockwise')
```

**Verification:**
```python
assert np.abs(np.mean(result2) - np.mean(result1)) < 1.0
```

### Step 4: Assign result2 = nlmeans(...)

```python
result2 = nlmeans(S0, sigma=np.array(1.0), method='blockwise')
```

**Verification:**
```python
assert result3.shape == S0.shape
```

### Step 5: Assign result3 = nlmeans(...)

```python
result3 = nlmeans(S0, sigma=np.array([1.0]), method='blockwise')
```

**Verification:**
```python
assert np.abs(np.mean(result3) - np.mean(result1)) < 1.0
```

### Step 6: Assign sigma_3d = value

```python
sigma_3d = np.ones(S0.shape) * 1.0
```

**Verification:**
```python
assert result4.shape == S0.shape
```

### Step 7: Assign result4 = nlmeans(...)

```python
result4 = nlmeans(S0, sigma=sigma_3d, method='blockwise')
```

**Verification:**
```python
assert np.abs(np.mean(result4) - np.mean(result1)) < 5.0
```


## Complete Example

```python
# Workflow
'\n    Test that blockwise method supports different sigma input formats.\n    '
S0 = 100 * np.ones((20, 20, 20), dtype='f8')
result1 = nlmeans(S0, sigma=1.0, method='blockwise')
assert result1.shape == S0.shape
result2 = nlmeans(S0, sigma=np.array(1.0), method='blockwise')
assert result2.shape == S0.shape
assert np.abs(np.mean(result2) - np.mean(result1)) < 1.0
result3 = nlmeans(S0, sigma=np.array([1.0]), method='blockwise')
assert result3.shape == S0.shape
assert np.abs(np.mean(result3) - np.mean(result1)) < 1.0
sigma_3d = np.ones(S0.shape) * 1.0
result4 = nlmeans(S0, sigma=sigma_3d, method='blockwise')
assert result4.shape == S0.shape
assert np.abs(np.mean(result4) - np.mean(result1)) < 5.0
```

## Next Steps


---

*Source: test_nlmeans.py:210 | Complexity: Intermediate | Last updated: 2026-05-18*