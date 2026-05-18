# How To: Join Expansion

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test join expansion

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pytest`
- `interfaces`
- `interfaces.utility`
- `interfaces.base`

**Setup Required:**
```python
# Fixtures: tmpdir, needed_outputs
```

## Step-by-Step Guide

### Step 1: Call tmpdir.chdir()

```python
tmpdir.chdir()
```

**Verification:**
```python
assert len(joins) == 1, 'The number of join result nodes is incorrect.'
```

### Step 2: Assign _products = value

```python
_products = []
```

**Verification:**
```python
assert len(result.nodes()) == 8, 'The number of expanded nodes is incorrect.'
```

### Step 3: Assign _sum_operands = value

```python
_sum_operands = []
```

**Verification:**
```python
assert len(_sums) == 1, 'The number of join outputs is incorrect'
```

### Step 4: Assign _sums = value

```python
_sums = []
```

**Verification:**
```python
assert _sums[0] == 7, 'The join Sum output value is incorrect: %s.' % _sums[0]
```

### Step 5: Assign prev_state = config.get(...)

```python
prev_state = config.get('execution', 'remove_unnecessary_outputs')
```

**Verification:**
```python
assert _sum_operands[0] == [3, 4], 'The join Sum input is incorrect: %s.' % _sum_operands[0]
```

### Step 6: Call config.set()

```python
config.set('execution', 'remove_unnecessary_outputs', needed_outputs)
```

**Verification:**
```python
assert len(_products) == 2, 'The number of iterated post-join outputs is incorrect'
```

### Step 7: Assign wf = pe.Workflow(...)

```python
wf = pe.Workflow(name='test')
```

### Step 8: Assign inputspec = pe.Node(...)

```python
inputspec = pe.Node(IdentityInterface(fields=['n']), name='inputspec')
```

### Step 9: Assign inputspec.iterables = value

```python
inputspec.iterables = [('n', [1, 2])]
```

### Step 10: Assign pre_join1 = pe.Node(...)

```python
pre_join1 = pe.Node(IncrementInterface(), name='pre_join1')
```

### Step 11: Assign pre_join2 = pe.Node(...)

```python
pre_join2 = pe.Node(IncrementInterface(), name='pre_join2')
```

### Step 12: Assign join = pe.JoinNode(...)

```python
join = pe.JoinNode(SumInterface(), joinsource='inputspec', joinfield='input1', name='join')
```

### Step 13: Assign post_join1 = pe.Node(...)

```python
post_join1 = pe.Node(IncrementInterface(), name='post_join1')
```

### Step 14: Assign post_join2 = pe.Node(...)

```python
post_join2 = pe.Node(ProductInterface(), name='post_join2')
```

### Step 15: Call wf.connect()

```python
wf.connect([(inputspec, pre_join1, [('n', 'input1')]), (pre_join1, pre_join2, [('output1', 'input1')]), (pre_join1, post_join2, [('output1', 'input2')]), (pre_join2, join, [('output1', 'input1')]), (join, post_join1, [('output1', 'input1')]), (join, post_join2, [('output1', 'input1')])])
```

### Step 16: Assign result = wf.run(...)

```python
result = wf.run()
```

### Step 17: Assign joins = value

```python
joins = [node for node in result.nodes() if node.name == 'join']
```

**Verification:**
```python
assert len(joins) == 1, 'The number of join result nodes is incorrect.'
```

### Step 18: Call config.set()

```python
config.set('execution', 'remove_unnecessary_outputs', prev_state)
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir, needed_outputs

# Workflow
global _sums
global _sum_operands
global _products
tmpdir.chdir()
_products = []
_sum_operands = []
_sums = []
prev_state = config.get('execution', 'remove_unnecessary_outputs')
config.set('execution', 'remove_unnecessary_outputs', needed_outputs)
wf = pe.Workflow(name='test')
inputspec = pe.Node(IdentityInterface(fields=['n']), name='inputspec')
inputspec.iterables = [('n', [1, 2])]
pre_join1 = pe.Node(IncrementInterface(), name='pre_join1')
pre_join2 = pe.Node(IncrementInterface(), name='pre_join2')
join = pe.JoinNode(SumInterface(), joinsource='inputspec', joinfield='input1', name='join')
post_join1 = pe.Node(IncrementInterface(), name='post_join1')
post_join2 = pe.Node(ProductInterface(), name='post_join2')
wf.connect([(inputspec, pre_join1, [('n', 'input1')]), (pre_join1, pre_join2, [('output1', 'input1')]), (pre_join1, post_join2, [('output1', 'input2')]), (pre_join2, join, [('output1', 'input1')]), (join, post_join1, [('output1', 'input1')]), (join, post_join2, [('output1', 'input1')])])
result = wf.run()
joins = [node for node in result.nodes() if node.name == 'join']
assert len(joins) == 1, 'The number of join result nodes is incorrect.'
assert len(result.nodes()) == 8, 'The number of expanded nodes is incorrect.'
assert len(_sums) == 1, 'The number of join outputs is incorrect'
assert _sums[0] == 7, 'The join Sum output value is incorrect: %s.' % _sums[0]
assert _sum_operands[0] == [3, 4], 'The join Sum input is incorrect: %s.' % _sum_operands[0]
assert len(_products) == 2, 'The number of iterated post-join outputs is incorrect'
config.set('execution', 'remove_unnecessary_outputs', prev_state)
```

## Next Steps


---

*Source: test_join.py:141 | Complexity: Advanced | Last updated: 2026-05-18*