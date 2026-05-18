# How To: Sample Does Not Rely On External Global Seeding

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test sample does not rely on external global seeding

## Prerequisites

**Required Modules:**
- `logging`
- `unittest.mock`
- `warnings`
- `contextlib`
- `numpy`
- `numpy.testing`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.special`
- `pytensor`
- `pytensor.compile.ops`
- `xarray`
- `pymc`
- `pymc.backends.ndarray`
- `pymc.distributions`
- `pymc.exceptions`
- `pymc.sampling.mcmc`
- `pymc.stats.convergence`
- `pymc.step_methods`
- `pymc.testing`
- `tests.models`


## Step-by-Step Guide

### Step 1: Assign kwargs = value

```python
kwargs = {'tune': 2, 'draws': 20, 'random_seed': None, 'return_inferencedata': False}
```

**Verification:**
```python
assert np.all(idata11['x'] != idata21['x'])
```

### Step 2: Call warnings.filterwarnings()

```python
warnings.filterwarnings('ignore', '.*number of samples.*', UserWarning)
```

**Verification:**
```python
assert np.all(idata12['x'] != idata22['x'])
```

### Step 3: Call np.random.seed()

```python
np.random.seed(1)
```

**Verification:**
```python
assert np.all(idata13['x'] != idata23['x'])
```

### Step 4: Assign idata11 = pm.sample(...)

```python
idata11 = pm.sample(chains=1, **kwargs)
```

### Step 5: Call np.random.seed()

```python
np.random.seed(1)
```

### Step 6: Assign idata12 = pm.sample(...)

```python
idata12 = pm.sample(chains=2, cores=1, **kwargs)
```

### Step 7: Call np.random.seed()

```python
np.random.seed(1)
```

### Step 8: Assign idata13 = pm.sample(...)

```python
idata13 = pm.sample(chains=2, cores=2, **kwargs)
```

### Step 9: Call np.random.seed()

```python
np.random.seed(1)
```

### Step 10: Assign idata21 = pm.sample(...)

```python
idata21 = pm.sample(chains=1, **kwargs)
```

### Step 11: Call np.random.seed()

```python
np.random.seed(1)
```

### Step 12: Assign idata22 = pm.sample(...)

```python
idata22 = pm.sample(chains=2, cores=1, **kwargs)
```

### Step 13: Call np.random.seed()

```python
np.random.seed(1)
```

### Step 14: Assign idata23 = pm.sample(...)

```python
idata23 = pm.sample(chains=2, cores=2, **kwargs)
```


## Complete Example

```python
# Workflow
kwargs = {'tune': 2, 'draws': 20, 'random_seed': None, 'return_inferencedata': False}
with self.model:
    with warnings.catch_warnings(), pytest.warns(FutureWarning, match='return_inferencedata=False'):
        warnings.filterwarnings('ignore', '.*number of samples.*', UserWarning)
        np.random.seed(1)
        idata11 = pm.sample(chains=1, **kwargs)
        np.random.seed(1)
        idata12 = pm.sample(chains=2, cores=1, **kwargs)
        np.random.seed(1)
        idata13 = pm.sample(chains=2, cores=2, **kwargs)
        np.random.seed(1)
        idata21 = pm.sample(chains=1, **kwargs)
        np.random.seed(1)
        idata22 = pm.sample(chains=2, cores=1, **kwargs)
        np.random.seed(1)
        idata23 = pm.sample(chains=2, cores=2, **kwargs)
assert np.all(idata11['x'] != idata21['x'])
assert np.all(idata12['x'] != idata22['x'])
assert np.all(idata13['x'] != idata23['x'])
```

## Next Steps


---

*Source: test_mcmc.py:124 | Complexity: Advanced | Last updated: 2026-05-18*