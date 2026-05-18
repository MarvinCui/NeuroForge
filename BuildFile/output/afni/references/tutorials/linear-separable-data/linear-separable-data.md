# How To: Linear Separable Data

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test linear separable data

## Prerequisites

**Required Modules:**
- `_tools`
- `svm`


## Step-by-Step Guide

### Step 1: Assign num_train = 100

```python
num_train = 100
```

**Verification:**
```python
assert svm_node.input_dim == len(traindata_real.T)
```

### Step 2: Assign num_test = 50

```python
num_test = 50
```

**Verification:**
```python
assert testerr, ('classification error for ', comb)
```

### Step 3: Assign C = 1.01

```python
C = 1.01
```

**Verification:**
```python
assert numx.all(pos1_rank == -pos2_rank)
```

### Step 4: Assign epsilon = 1e-05

```python
epsilon = 1e-05
```

**Verification:**
```python
assert numx.all(abs(pos1_rank) == 1)
```

### Step 5: Assign radius = 0.3

```python
radius = 0.3
```

**Verification:**
```python
assert numx.all(abs(pos2_rank) == 1)
```

### Step 6: Assign unknown = _separable_data(...)

```python
traindata_real, trainlab = _separable_data(positions, (-1, 1), radius, num_train, True)
```

### Step 7: Assign unknown = _separable_data(...)

```python
testdata_real, testlab = _separable_data(positions, (-1, 1), radius, num_test, True)
```

### Step 8: Assign svm_node = mdp.nodes.LibSVMClassifier(...)

```python
svm_node = mdp.nodes.LibSVMClassifier(kernel=comb['kernel'], classifier=comb['classifier'], probability=True, params={'C': C, 'eps': epsilon})
```

### Step 9: Call svm_node.train()

```python
svm_node.train(traindata_real[:num_train], trainlab[:num_train])
```

### Step 10: Call svm_node.train()

```python
svm_node.train(traindata_real[num_train:], trainlab[num_train:])
```

**Verification:**
```python
assert svm_node.input_dim == len(traindata_real.T)
```

### Step 11: Assign out = svm_node.label(...)

```python
out = svm_node.label(testdata_real)
```

### Step 12: Assign testerr = numx.all(...)

```python
testerr = numx.all(numx.sign(out) == testlab)
```

**Verification:**
```python
assert testerr, ('classification error for ', comb)
```

### Step 13: Assign pos1_rank = numx.array(...)

```python
pos1_rank = numx.array(svm_node.rank(numx.array([positions[0]])))
```

### Step 14: Assign pos2_rank = numx.array(...)

```python
pos2_rank = numx.array(svm_node.rank(numx.array([positions[1]])))
```

**Verification:**
```python
assert numx.all(pos1_rank == -pos2_rank)
```


## Complete Example

```python
# Workflow
num_train = 100
num_test = 50
C = 1.01
epsilon = 1e-05
for positions in [((1,), (-1,)), ((1, 1), (-1, -1)), ((1, 1, 1), (-1, -1, 1)), ((1, 1, 1, 1), (-1, 1, 1, 1)), ((1, 1, 1, 1), (-1, -1, -1, -1))]:
    radius = 0.3
    traindata_real, trainlab = _separable_data(positions, (-1, 1), radius, num_train, True)
    testdata_real, testlab = _separable_data(positions, (-1, 1), radius, num_test, True)
    for comb in utils.orthogonal_permutations(self.combinations):
        if comb['classifier'] in ['ONE_CLASS']:
            continue
        if comb['kernel'] in ['SIGMOID', 'POLY']:
            continue
        if len(positions[0]) == 1 and comb['kernel'] == 'RBF':
            continue
        svm_node = mdp.nodes.LibSVMClassifier(kernel=comb['kernel'], classifier=comb['classifier'], probability=True, params={'C': C, 'eps': epsilon})
        svm_node.train(traindata_real[:num_train], trainlab[:num_train])
        svm_node.train(traindata_real[num_train:], trainlab[num_train:])
        assert svm_node.input_dim == len(traindata_real.T)
        out = svm_node.label(testdata_real)
        testerr = numx.all(numx.sign(out) == testlab)
        assert testerr, ('classification error for ', comb)
        if not comb['classifier'].endswith('SVR'):
            pos1_rank = numx.array(svm_node.rank(numx.array([positions[0]])))
            pos2_rank = numx.array(svm_node.rank(numx.array([positions[1]])))
            assert numx.all(pos1_rank == -pos2_rank)
            assert numx.all(abs(pos1_rank) == 1)
            assert numx.all(abs(pos2_rank) == 1)
```

## Next Steps


---

*Source: test_svm_classifier.py:219 | Complexity: Advanced | Last updated: 2026-05-18*