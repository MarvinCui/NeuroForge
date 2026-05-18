# How To: Tequiv

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test t-test equivalence.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `functools`
- `itertools`
- `numpy`
- `pytest`
- `scipy.stats`
- `numpy.testing`
- `mne`
- `mne.stats.parametric`

**Setup Required:**
```python
# Fixtures: kind, kwargs, sigma, seed
```

## Step-by-Step Guide

### Step 1: 'Test t-test equivalence.'

```python
'Test t-test equivalence.'
```

**Verification:**
```python
assert_allclose(got, want, rtol=1e-07, atol=1e-06)
```

### Step 2: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(seed)
```

**Verification:**
```python
assert not np.allclose(got, want, rtol=1e-07, atol=1e-06)
```

### Step 3: Assign ours = partial(...)

```python
ours = partial(getattr(mne.stats, f'ttest_{kind}_no_p'), sigma=sigma, **kwargs)
```

**Verification:**
```python
assert_allclose(got, want, rtol=0.2, atol=0.01)
```

### Step 4: Assign X = rng.randn(...)

```python
X = rng.randn(3, 4, 5)
```

**Verification:**
```python
assert_array_less(np.abs(got), np.abs(want))
```

### Step 5: Assign f = getattr(...)

```python
f = getattr(scipy.stats, f'ttest_{kind}')
```

### Step 6: Assign X = value

```python
X = [X, rng.randn(30, 4, 5)]
```

### Step 7: Assign got = ours(...)

```python
got = ours(*X)
```

### Step 8: Assign want = theirs(...)

```python
want = theirs(*X)
```

### Step 9: Assign got = ours(...)

```python
got = ours(X)
```

### Step 10: Assign want = theirs(...)

```python
want = theirs(X)
```

### Step 11: Call assert_allclose()

```python
assert_allclose(got, want, rtol=1e-07, atol=1e-06)
```

**Verification:**
```python
assert not np.allclose(got, want, rtol=1e-07, atol=1e-06)
```

### Step 12: Call assert_allclose()

```python
assert_allclose(got, want, rtol=0.2, atol=0.01)
```

### Step 13: Call assert_array_less()

```python
assert_array_less(np.abs(got), np.abs(want))
```

### Step 14: Assign func = partial(...)

```python
func = partial(f, popmean=0, **kwargs)
```

### Step 15: Assign func = partial(...)

```python
func = partial(f, **kwargs)
```


## Complete Example

```python
# Setup
# Fixtures: kind, kwargs, sigma, seed

# Workflow
'Test t-test equivalence.'
rng = np.random.RandomState(seed)

def theirs(*a, **kw):
    f = getattr(scipy.stats, f'ttest_{kind}')
    if kind == '1samp':
        func = partial(f, popmean=0, **kwargs)
    else:
        func = partial(f, **kwargs)
    return func(*a, **kw)[0]
ours = partial(getattr(mne.stats, f'ttest_{kind}_no_p'), sigma=sigma, **kwargs)
X = rng.randn(3, 4, 5)
if kind == 'ind':
    X = [X, rng.randn(30, 4, 5)]
    got = ours(*X)
    want = theirs(*X)
else:
    got = ours(X)
    want = theirs(X)
if sigma == 0.0:
    assert_allclose(got, want, rtol=1e-07, atol=1e-06)
else:
    assert not np.allclose(got, want, rtol=1e-07, atol=1e-06)
    assert_allclose(got, want, rtol=0.2, atol=0.01)
    assert_array_less(np.abs(got), np.abs(want))
```

## Next Steps


---

*Source: test_parametric.py:148 | Complexity: Advanced | Last updated: 2026-05-18*