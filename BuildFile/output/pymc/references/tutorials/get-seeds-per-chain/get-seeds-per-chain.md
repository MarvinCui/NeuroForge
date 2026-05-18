# How To: Get Seeds Per Chain

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test get seeds per chain

## Prerequisites

**Required Modules:**
- `re`
- `arviz`
- `numpy`
- `pytest`
- `xarray`
- `cachetools`
- `pymc`
- `pymc.distributions.transforms`
- `pymc.util`


## Step-by-Step Guide

### Step 1: Assign ret = _get_seeds_per_chain(...)

```python
ret = _get_seeds_per_chain(None, chains=1)
```

**Verification:**
```python
assert len(ret) == 1 and isinstance(ret[0], int)
```

### Step 2: Assign ret = _get_seeds_per_chain(...)

```python
ret = _get_seeds_per_chain(None, chains=2)
```

**Verification:**
```python
assert len(ret) == 2 and isinstance(ret[0], int)
```

### Step 3: Assign ret = _get_seeds_per_chain(...)

```python
ret = _get_seeds_per_chain(5, chains=1)
```

**Verification:**
```python
assert ret == (5,)
```

### Step 4: Assign ret = _get_seeds_per_chain(...)

```python
ret = _get_seeds_per_chain(5, chains=3)
```

**Verification:**
```python
assert len(ret) == 3 and isinstance(ret[0], int) and (not any((r == 5 for r in ret)))
```

### Step 5: Assign rng = np.random.default_rng(...)

```python
rng = np.random.default_rng(123)
```

**Verification:**
```python
assert ret == expected_ret
```

### Step 6: Assign expected_ret = rng.integers(...)

```python
expected_ret = rng.integers(2 ** 30, dtype=np.int64, size=1)
```

**Verification:**
```python
assert np.all(ret == expected_ret)
```

### Step 7: Assign rng = np.random.default_rng(...)

```python
rng = np.random.default_rng(123)
```

**Verification:**
```python
assert ret is expected_ret
```

### Step 8: Assign ret = _get_seeds_per_chain(...)

```python
ret = _get_seeds_per_chain(rng, chains=1)
```

**Verification:**
```python
assert ret == expected_ret
```

### Step 9: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(456)
```

### Step 10: Assign expected_ret = rng.randint(...)

```python
expected_ret = rng.randint(2 ** 30, dtype=np.int64, size=2)
```

### Step 11: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(456)
```

### Step 12: Assign ret = _get_seeds_per_chain(...)

```python
ret = _get_seeds_per_chain(rng, chains=2)
```

**Verification:**
```python
assert np.all(ret == expected_ret)
```

### Step 13: Assign ret = _get_seeds_per_chain(...)

```python
ret = _get_seeds_per_chain(expected_ret, chains=len(expected_ret))
```

**Verification:**
```python
assert ret is expected_ret
```

### Step 14: Call _get_seeds_per_chain()

```python
_get_seeds_per_chain({1: 1, 2: 2}, 2)
```

### Step 15: Call _get_seeds_per_chain()

```python
_get_seeds_per_chain(expected_ret, chains=len(expected_ret) + 1)
```


## Complete Example

```python
# Workflow
ret = _get_seeds_per_chain(None, chains=1)
assert len(ret) == 1 and isinstance(ret[0], int)
ret = _get_seeds_per_chain(None, chains=2)
assert len(ret) == 2 and isinstance(ret[0], int)
ret = _get_seeds_per_chain(5, chains=1)
assert ret == (5,)
ret = _get_seeds_per_chain(5, chains=3)
assert len(ret) == 3 and isinstance(ret[0], int) and (not any((r == 5 for r in ret)))
rng = np.random.default_rng(123)
expected_ret = rng.integers(2 ** 30, dtype=np.int64, size=1)
rng = np.random.default_rng(123)
ret = _get_seeds_per_chain(rng, chains=1)
assert ret == expected_ret
rng = np.random.RandomState(456)
expected_ret = rng.randint(2 ** 30, dtype=np.int64, size=2)
rng = np.random.RandomState(456)
ret = _get_seeds_per_chain(rng, chains=2)
assert np.all(ret == expected_ret)
for expected_ret in ([0, 1, 2], (0, 1, 2, 3), np.arange(5)):
    ret = _get_seeds_per_chain(expected_ret, chains=len(expected_ret))
    assert ret is expected_ret
    with pytest.raises(ValueError, match='does not match the number of chains'):
        _get_seeds_per_chain(expected_ret, chains=len(expected_ret) + 1)
with pytest.raises(ValueError, match=re.escape('The `seeds` must be array-like')):
    _get_seeds_per_chain({1: 1, 2: 2}, 2)
```

## Next Steps


---

*Source: test_util.py:192 | Complexity: Advanced | Last updated: 2026-05-18*