# How To: Upstream Rngs Not In Compiled Logp

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test upstream rngs not in compiled logp

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `sys`
- `warnings`
- `cloudpickle`
- `numpy`
- `pytensor`
- `pytest`
- `scipy.stats`
- `pytensor.compile.mode`
- `pytensor.graph`
- `pytensor.link.numba`
- `pytensor.tensor.random.op`
- `pytensor.tensor.random.variable`
- `pytensor.tensor.sort`
- `pymc`
- `pymc.initial_point`
- `pymc.pytensorf`
- `pymc.smc.kernels`

**Setup Required:**
```python
# Fixtures: seeded_test
```

## Step-by-Step Guide

### Step 1: Assign smc = IMH(...)

```python
smc = IMH(model=self.SMABC_test)
```

**Verification:**
```python
assert likelihood_func(inarray) != likelihood_func(inarray)
```

### Step 2: Call smc.initialize_population()

```python
smc.initialize_population()
```

**Verification:**
```python
assert len(shared_rng_vars) == 1
```

### Step 3: Call smc._initialize_kernel()

```python
smc._initialize_kernel()
```

### Step 4: Assign likelihood_func = value

```python
likelihood_func = smc.likelihood_logp_func
```

### Step 5: Assign inarray = floatX(...)

```python
inarray = floatX(np.array([0, 0]))
```

**Verification:**
```python
assert likelihood_func(inarray) != likelihood_func(inarray)
```

### Step 6: Assign compiled_graph = value

```python
compiled_graph = likelihood_func.maker.fgraph.outputs
```

### Step 7: Assign shared_rng_vars = value

```python
shared_rng_vars = [node for node in ancestors(compiled_graph) if isinstance(node, RandomGeneratorSharedVariable)]
```

**Verification:**
```python
assert len(shared_rng_vars) == 1
```


## Complete Example

```python
# Setup
# Fixtures: seeded_test

# Workflow
smc = IMH(model=self.SMABC_test)
smc.initialize_population()
smc._initialize_kernel()
likelihood_func = smc.likelihood_logp_func
inarray = floatX(np.array([0, 0]))
assert likelihood_func(inarray) != likelihood_func(inarray)
compiled_graph = likelihood_func.maker.fgraph.outputs
shared_rng_vars = [node for node in ancestors(compiled_graph) if isinstance(node, RandomGeneratorSharedVariable)]
assert len(shared_rng_vars) == 1
```

## Next Steps


---

*Source: test_simulator.py:257 | Complexity: Intermediate | Last updated: 2026-05-18*