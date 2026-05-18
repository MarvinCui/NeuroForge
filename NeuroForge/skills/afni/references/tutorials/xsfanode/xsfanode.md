# How To: Xsfanode

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test XSFANode

## Prerequisites

**Required Modules:**
- `_tools`
- `test_ICANode`


## Step-by-Step Guide

### Step 1: Assign T = 5000

```python
T = 5000
```

**Verification:**
```python
assert min(corrs) > 0.8, 'source/estimate minimal covariance: %g' % min(corrs)
```

### Step 2: Assign N = 3

```python
N = 3
```

### Step 3: Assign src = value

```python
src = numx_rand.random((T, N)) * 2 - 1
```

### Step 4: Assign fsrc = numx_fft.rfft(...)

```python
fsrc = numx_fft.rfft(src, axis=0)
```

### Step 5: Assign src = numx_fft.irfft(...)

```python
src = numx_fft.irfft(fsrc, axis=0)
```

### Step 6: Assign mix = src

```python
mix = src
```

### Step 7: Assign flow = mdp.Flow(...)

```python
flow = mdp.Flow([mdp.nodes.XSFANode()])
```

### Step 8: Call flow.train()

```python
flow.train([[mix[:T / 2, :], mix[T / 2:, :]]])
```

### Step 9: Assign out = flow(...)

```python
out = flow(mix)
```

### Step 10: Assign corrs = mdp.utils.cov_maxima(...)

```python
corrs = mdp.utils.cov_maxima(mdp.utils.cov2(out, src))
```

**Verification:**
```python
assert min(corrs) > 0.8, 'source/estimate minimal covariance: %g' % min(corrs)
```

### Step 11: Assign unknown = 0.0

```python
fsrc[(i + 1) * (T / 10):, i] = 0.0
```


## Complete Example

```python
# Workflow
T = 5000
N = 3
src = numx_rand.random((T, N)) * 2 - 1
fsrc = numx_fft.rfft(src, axis=0)
for i in xrange(N):
    fsrc[(i + 1) * (T / 10):, i] = 0.0
src = numx_fft.irfft(fsrc, axis=0)
src -= src.mean(axis=0)
src /= src.std(axis=0)
mix = src
flow = mdp.Flow([mdp.nodes.XSFANode()])
flow.train([[mix[:T / 2, :], mix[T / 2:, :]]])
out = flow(mix)
corrs = mdp.utils.cov_maxima(mdp.utils.cov2(out, src))
assert min(corrs) > 0.8, 'source/estimate minimal covariance: %g' % min(corrs)
```

## Next Steps


---

*Source: test_contrib.py:198 | Complexity: Advanced | Last updated: 2026-05-18*