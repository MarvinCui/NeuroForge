# How To: Nipalsnode Desired Variance

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test NIPALSNode desired variance

## Prerequisites

**Required Modules:**
- `_tools`
- `test_ICANode`


## Step-by-Step Guide

### Step 1: Assign unknown = get_random_mix(...)

```python
mat, mix, inp = get_random_mix(mat_dim=(1000, 3))
```

**Verification:**
```python
assert pca.output_dim == 2
```

### Step 2: Assign pca = mdp.nodes.WhiteningNode(...)

```python
pca = mdp.nodes.WhiteningNode()
```

**Verification:**
```python
assert out.shape[1] == 2
```

### Step 3: Call pca.train()

```python
pca.train(mat)
```

**Verification:**
```python
assert pca.explained_variance > 0.8 and pca.explained_variance < 1
```

### Step 4: Assign mat = pca.execute(...)

```python
mat = pca.execute(mat)
```

### Step 5: Assign pca = mdp.nodes.NIPALSNode(...)

```python
pca = mdp.nodes.NIPALSNode(output_dim=0.8)
```

### Step 6: Call pca.train()

```python
pca.train(mat)
```

### Step 7: Assign out = pca.execute(...)

```python
out = pca.execute(mat)
```

**Verification:**
```python
assert pca.output_dim == 2
```


## Complete Example

```python
# Workflow
mat, mix, inp = get_random_mix(mat_dim=(1000, 3))
pca = mdp.nodes.WhiteningNode()
pca.train(mat)
mat = pca.execute(mat)
mat *= [0.6, 0.3, 0.1]
pca = mdp.nodes.NIPALSNode(output_dim=0.8)
pca.train(mat)
out = pca.execute(mat)
assert pca.output_dim == 2
assert out.shape[1] == 2
assert pca.explained_variance > 0.8 and pca.explained_variance < 1
```

## Next Steps


---

*Source: test_contrib.py:91 | Complexity: Intermediate | Last updated: 2026-05-18*