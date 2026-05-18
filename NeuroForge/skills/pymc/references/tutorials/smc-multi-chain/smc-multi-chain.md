# How To: Smc Multi Chain

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test smc multi chain

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `unittest.mock`
- `pytest`
- `pymc`
- `pymc.progress_bar`
- `pymc.smc.kernels`
- `pymc.step_methods`

**Setup Required:**
```python
# Fixtures: imh_kernel
```

## Step-by-Step Guide

### Step 1: Assign chains = 3

```python
chains = 3
```

**Verification:**
```python
assert _get_task(manager, chain).completed == 0
```

### Step 2: Assign manager = SMCProgressBarManager(...)

```python
manager = SMCProgressBarManager(kernel=imh_kernel, chains=chains, progressbar=True)
```

**Verification:**
```python
assert _get_task(manager, chain).completed == pytest.approx(1.0)
```

### Step 3: Call manager.update()

```python
manager.update(chain_idx=chain, stage=0, beta=0.4, old_beta=0.0)
```

### Step 4: Call manager.update()

```python
manager.update(chain_idx=chain, stage=1, beta=1.0, old_beta=0.4, is_last=True)
```

**Verification:**
```python
assert _get_task(manager, chain).completed == pytest.approx(1.0)
```


## Complete Example

```python
# Setup
# Fixtures: imh_kernel

# Workflow
chains = 3
manager = SMCProgressBarManager(kernel=imh_kernel, chains=chains, progressbar=True)
with manager:
    for chain in range(chains):
        assert _get_task(manager, chain).completed == 0
    for chain in range(chains):
        manager.update(chain_idx=chain, stage=0, beta=0.4, old_beta=0.0)
        manager.update(chain_idx=chain, stage=1, beta=1.0, old_beta=0.4, is_last=True)
    for chain in range(chains):
        assert _get_task(manager, chain).completed == pytest.approx(1.0)
```

## Next Steps


---

*Source: test_manager.py:143 | Complexity: Intermediate | Last updated: 2026-05-18*