# How To: Output Dim Bug

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test output dim bug

## Prerequisites

**Required Modules:**
- `_tools`


## Step-by-Step Guide

### Step 1: Assign dim = 10000

```python
dim = 10000
```

**Verification:**
```python
assert out.shape[1] == 3
```

### Step 2: Assign freqs = value

```python
freqs = [2 * numx.pi * 100.0, 2 * numx.pi * 500.0]
```

### Step 3: Assign t = numx.linspace(...)

```python
t = numx.linspace(0, 1, num=dim)
```

### Step 4: Assign mat = value

```python
mat = numx.array([numx.sin(freqs[0] * t), numx.sin(freqs[1] * t)]).T
```

### Step 5: Assign mat = value

```python
mat = (mat - mean(mat[:-1, :], axis=0)) / std(mat[:-1, :], axis=0)
```

### Step 6: Assign mat = value

```python
mat = mult(mat, uniform((2, 2))) + uniform(2)
```

### Step 7: Assign sfa = mdp.nodes.SFA2Node(...)

```python
sfa = mdp.nodes.SFA2Node(output_dim=3)
```

### Step 8: Call sfa.train()

```python
sfa.train(mat)
```

### Step 9: Assign out = sfa.execute(...)

```python
out = sfa.execute(mat)
```

**Verification:**
```python
assert out.shape[1] == 3
```


## Complete Example

```python
# Workflow
dim = 10000
freqs = [2 * numx.pi * 100.0, 2 * numx.pi * 500.0]
t = numx.linspace(0, 1, num=dim)
mat = numx.array([numx.sin(freqs[0] * t), numx.sin(freqs[1] * t)]).T
mat += normal(0.0, 1e-10, size=(dim, 2))
mat = (mat - mean(mat[:-1, :], axis=0)) / std(mat[:-1, :], axis=0)
mat = mult(mat, uniform((2, 2))) + uniform(2)
sfa = mdp.nodes.SFA2Node(output_dim=3)
sfa.train(mat)
out = sfa.execute(mat)
assert out.shape[1] == 3
```

## Next Steps


---

*Source: test_SFA2Node.py:55 | Complexity: Advanced | Last updated: 2026-05-18*