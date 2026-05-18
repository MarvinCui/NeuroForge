# How To: Reseed Rngs

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test reseed rngs

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.ma`
- `numpy.testing`
- `pandas`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.sparse`
- `pytensor`
- `pytensor.compile`
- `pytensor.compile.builders`
- `pytensor.graph.basic`
- `pytensor.link.vm`
- `pytensor.tensor.subtensor`
- `pymc`
- `pymc.data`
- `pymc.distributions.dist_math`
- `pymc.distributions.distribution`
- `pymc.exceptions`
- `pymc.logprob.utils`
- `pymc.pytensorf`
- `pymc.vartypes`
- `cloudpickle`


## Step-by-Step Guide

### Step 1: Assign default_rng = value

```python
default_rng = np.random.PCG64
```

**Verification:**
```python
assert isinstance(np.random.default_rng().bit_generator, default_rng)
```

### Step 2: Assign seed = 543

```python
seed = 543
```

**Verification:**
```python
assert rng.get_value().bit_generator.state != bit_generator.state
```

### Step 3: Assign bit_generators = value

```python
bit_generators = [default_rng(sub_seed) for sub_seed in np.random.SeedSequence(seed).spawn(2)]
```

**Verification:**
```python
assert rng.get_value().bit_generator.state == bit_generator.state
```

### Step 4: Assign rngs = value

```python
rngs = [pytensor.shared(np.random.Generator(default_rng())) for _ in range(2)]
```

### Step 5: Call reseed_rngs()

```python
reseed_rngs(rngs, seed)
```

**Verification:**
```python
assert rng.get_value().bit_generator.state != bit_generator.state
```


## Complete Example

```python
# Workflow
default_rng = np.random.PCG64
assert isinstance(np.random.default_rng().bit_generator, default_rng)
seed = 543
bit_generators = [default_rng(sub_seed) for sub_seed in np.random.SeedSequence(seed).spawn(2)]
rngs = [pytensor.shared(np.random.Generator(default_rng())) for _ in range(2)]
for rng, bit_generator in zip(rngs, bit_generators):
    assert rng.get_value().bit_generator.state != bit_generator.state
reseed_rngs(rngs, seed)
for rng, bit_generator in zip(rngs, bit_generators):
    assert rng.get_value().bit_generator.state == bit_generator.state
```

## Next Steps


---

*Source: test_pytensorf.py:624 | Complexity: Intermediate | Last updated: 2026-05-18*