# How To: Variadiccumulator

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test VariadicCumulator

## Prerequisites

**Required Modules:**
- `mdp`
- `_tools`


## Step-by-Step Guide

### Step 1: Assign ONELEN = 101

```python
ONELEN = 101
```

**Verification:**
```python
assert hasattr(self, 'a')
```

### Step 2: Assign NREP = 7

```python
NREP = 7
```

**Verification:**
```python
assert hasattr(self, 'b')
```

### Step 3: Assign x = value

```python
x = [numx_rand.rand(ONELEN, 3) for _ in range(NREP)]
```

**Verification:**
```python
assert self.tlen == tlen
```

### Step 4: Assign y = value

```python
y = [numx_rand.rand(ONELEN, 3) for _ in range(NREP)]
```

**Verification:**
```python
assert self.a.shape == (tlen, 3)
```

### Step 5: Assign ABCumulator = mdp.VariadicCumulator(...)

```python
ABCumulator = mdp.VariadicCumulator('a', 'b')
```

**Verification:**
```python
assert self.b.shape == (tlen, 3)
```

### Step 6: Assign ab = TestABCumulator(...)

```python
ab = TestABCumulator()
```

**Verification:**
```python
assert numx.all(self.a[i * ONELEN:(i + 1) * ONELEN, :] == x[i])
```

### Step 7: Call ab.stop_training()

```python
ab.stop_training()
```

**Verification:**
```python
assert numx.all(self.b[i * ONELEN:(i + 1) * ONELEN, :] == y[i])
```

### Step 8: Call ab.train()

```python
ab.train(x[i], y[i])
```

### Step 9: Call super._stop_training()

```python
super(TestABCumulator, self)._stop_training(*args, **kwargs)
```

**Verification:**
```python
assert hasattr(self, 'a')
```

### Step 10: Assign tlen = value

```python
tlen = ONELEN * NREP
```

**Verification:**
```python
assert self.tlen == tlen
```


## Complete Example

```python
# Workflow
ONELEN = 101
NREP = 7
x = [numx_rand.rand(ONELEN, 3) for _ in range(NREP)]
y = [numx_rand.rand(ONELEN, 3) for _ in range(NREP)]
ABCumulator = mdp.VariadicCumulator('a', 'b')

class TestABCumulator(ABCumulator):

    def _stop_training(self, *args, **kwargs):
        super(TestABCumulator, self)._stop_training(*args, **kwargs)
        assert hasattr(self, 'a')
        assert hasattr(self, 'b')
        tlen = ONELEN * NREP
        assert self.tlen == tlen
        assert self.a.shape == (tlen, 3)
        assert self.b.shape == (tlen, 3)
        for i in range(NREP):
            assert numx.all(self.a[i * ONELEN:(i + 1) * ONELEN, :] == x[i])
            assert numx.all(self.b[i * ONELEN:(i + 1) * ONELEN, :] == y[i])
ab = TestABCumulator()
for i in range(NREP):
    ab.train(x[i], y[i])
ab.stop_training()
```

## Next Steps


---

*Source: test_VariadicCumulator.py:4 | Complexity: Advanced | Last updated: 2026-05-18*