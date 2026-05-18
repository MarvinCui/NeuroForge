# How To: Neuralgasnode

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test NeuralGasNode

## Prerequisites

**Required Modules:**
- `_tools`


## Step-by-Step Guide

### Step 1: Assign dim = 10

```python
dim = 10
```

**Verification:**
```python
assert max(numx.minimum(numx.sum(abs(poss - dir), axis=1), numx.sum(abs(poss + dir), axis=1))) < 1e-07, 'At least one node of the graph does lies out of the line.'
```

### Step 2: Assign npoints = 1000

```python
npoints = 1000
```

**Verification:**
```python
assert_equal(deg[:2], [1, 1])
```

### Step 3: Assign const = _uniform(...)

```python
const = _uniform(-100, 100, [dim])
```

**Verification:**
```python
assert_array_equal(deg[2:], [2 for i in xrange(len(deg) - 2)])
```

### Step 4: Assign dir = _uniform(...)

```python
dir = _uniform(-1, 1, [dim])
```

**Verification:**
```python
assert_almost_equal(dist, mean(dists), 1)
```

### Step 5: Assign x = _uniform(...)

```python
x = _uniform(-1, 1, [npoints])
```

### Step 6: Assign data = value

```python
data = numx.outer(x, dir) + const
```

### Step 7: Assign num_nodes = 10

```python
num_nodes = 10
```

### Step 8: Assign ng = mdp.nodes.NeuralGasNode(...)

```python
ng = mdp.nodes.NeuralGasNode(start_poss=[data[n, :] for n in range(num_nodes)], max_epochs=10)
```

### Step 9: Call ng.train()

```python
ng.train(data)
```

### Step 10: Call ng.stop_training()

```python
ng.stop_training()
```

### Step 11: Assign poss = value

```python
poss = ng.get_nodes_position() - const
```

### Step 12: Assign norms = numx.sqrt(...)

```python
norms = numx.sqrt(numx.sum(poss * poss, axis=1))
```

### Step 13: Assign poss = value

```python
poss = (poss.T / norms).T
```

**Verification:**
```python
assert max(numx.minimum(numx.sum(abs(poss - dir), axis=1), numx.sum(abs(poss + dir), axis=1))) < 1e-07, 'At least one node of the graph does lies out of the line.'
```

### Step 14: Assign topolist = ng.graph.topological_sort(...)

```python
topolist = ng.graph.topological_sort()
```

### Step 15: Assign deg = numx.asarray(...)

```python
deg = numx.asarray(map(lambda n: n.degree(), topolist))
```

### Step 16: Assign idx = deg.argsort(...)

```python
idx = deg.argsort()
```

### Step 17: Assign deg = value

```python
deg = deg[idx]
```

### Step 18: Call assert_equal()

```python
assert_equal(deg[:2], [1, 1])
```

### Step 19: Call assert_array_equal()

```python
assert_array_equal(deg[2:], [2 for i in xrange(len(deg) - 2)])
```

### Step 20: Assign x0 = value

```python
x0 = numx.outer(numx.amin(x, axis=0), dir) + const
```

### Step 21: Assign x1 = value

```python
x1 = numx.outer(numx.amax(x, axis=0), dir) + const
```

### Step 22: Assign linelen = utils.norm2(...)

```python
linelen = utils.norm2(x0 - x1)
```

### Step 23: Assign dist = value

```python
dist = linelen / poss.shape[0]
```

### Step 24: Assign nodes = ng.graph.undirected_dfs(...)

```python
nodes = ng.graph.undirected_dfs(topolist[idx[0]])
```

### Step 25: Assign poss = numx.array(...)

```python
poss = numx.array(map(lambda n: n.data.pos, nodes))
```

### Step 26: Assign dists = numx.sqrt(...)

```python
dists = numx.sqrt(numx.sum((poss[:-1, :] - poss[1:, :]) ** 2, axis=1))
```

### Step 27: Call assert_almost_equal()

```python
assert_almost_equal(dist, mean(dists), 1)
```


## Complete Example

```python
# Workflow
dim = 10
npoints = 1000
const = _uniform(-100, 100, [dim])
dir = _uniform(-1, 1, [dim])
dir /= utils.norm2(dir)
x = _uniform(-1, 1, [npoints])
data = numx.outer(x, dir) + const
num_nodes = 10
ng = mdp.nodes.NeuralGasNode(start_poss=[data[n, :] for n in range(num_nodes)], max_epochs=10)
ng.train(data)
ng.stop_training()
poss = ng.get_nodes_position() - const
norms = numx.sqrt(numx.sum(poss * poss, axis=1))
poss = (poss.T / norms).T
assert max(numx.minimum(numx.sum(abs(poss - dir), axis=1), numx.sum(abs(poss + dir), axis=1))) < 1e-07, 'At least one node of the graph does lies out of the line.'
topolist = ng.graph.topological_sort()
deg = numx.asarray(map(lambda n: n.degree(), topolist))
idx = deg.argsort()
deg = deg[idx]
assert_equal(deg[:2], [1, 1])
assert_array_equal(deg[2:], [2 for i in xrange(len(deg) - 2)])
x0 = numx.outer(numx.amin(x, axis=0), dir) + const
x1 = numx.outer(numx.amax(x, axis=0), dir) + const
linelen = utils.norm2(x0 - x1)
dist = linelen / poss.shape[0]
nodes = ng.graph.undirected_dfs(topolist[idx[0]])
poss = numx.array(map(lambda n: n.data.pos, nodes))
dists = numx.sqrt(numx.sum((poss[:-1, :] - poss[1:, :]) ** 2, axis=1))
assert_almost_equal(dist, mean(dists), 1)
```

## Next Steps


---

*Source: test_NeuralGasNode.py:6 | Complexity: Advanced | Last updated: 2026-05-18*