# How To: Mcmc Combined Bar Ends At Total

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test mcmc combined bar ends at total

## Prerequisites

**Required Modules:**
- `unittest.mock`
- `pytest`
- `pymc`
- `pymc.progress_bar`
- `pymc.smc.kernels`
- `pymc.step_methods`


## Step-by-Step Guide

### Step 1: Assign unknown = value

```python
draws, tune, chains = (10, 5, 2)
```

**Verification:**
```python
assert task.completed == task.total == total
```

### Step 2: Assign captured = value

```python
captured = {}
```

**Verification:**
```python
assert task.fields['draw'] == total
```

### Step 3: Assign orig_init = value

```python
orig_init = MCMCProgressBarManager.__init__
```

### Step 4: Assign manager = value

```python
manager = captured['manager']
```

### Step 5: Assign total = value

```python
total = (draws + tune) * chains
```

### Step 6: Assign task = _get_task(...)

```python
task = _get_task(manager, 0)
```

**Verification:**
```python
assert task.completed == task.total == total
```

### Step 7: Call orig_init()

```python
orig_init(self, *args, **kwargs)
```

### Step 8: Assign unknown = self

```python
captured['manager'] = self
```

### Step 9: Call pm.Normal()

```python
pm.Normal('x')
```

### Step 10: Call pm.sample()

```python
pm.sample(draws=draws, tune=tune, chains=chains, cores=1, progressbar='combined+stats', compute_convergence_checks=False, nuts_sampler='pymc')
```


## Complete Example

```python
# Workflow
draws, tune, chains = (10, 5, 2)
captured = {}
orig_init = MCMCProgressBarManager.__init__

def capturing_init(self, *args, **kwargs):
    orig_init(self, *args, **kwargs)
    captured['manager'] = self
with patch.object(MCMCProgressBarManager, '__init__', capturing_init):
    with pm.Model():
        pm.Normal('x')
        pm.sample(draws=draws, tune=tune, chains=chains, cores=1, progressbar='combined+stats', compute_convergence_checks=False, nuts_sampler='pymc')
manager = captured['manager']
total = (draws + tune) * chains
task = _get_task(manager, 0)
assert task.completed == task.total == total
assert task.fields['draw'] == total
```

## Next Steps


---

*Source: test_manager.py:72 | Complexity: Advanced | Last updated: 2026-05-18*