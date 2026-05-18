# How To: Itersource Join Source Node

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test join on an input node which has an ``itersource``.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pytest`
- `interfaces`
- `interfaces.utility`
- `interfaces.base`

**Setup Required:**
```python
# Fixtures: tmpdir
```

## Step-by-Step Guide

### Step 1: 'Test join on an input node which has an ``itersource``.'

```python
'Test join on an input node which has an ``itersource``.'
```

**Verification:**
```python
assert len(result.nodes()) == 14, 'The number of expanded nodes is incorrect.'
```

### Step 2: Call tmpdir.chdir()

```python
tmpdir.chdir()
```

**Verification:**
```python
assert [16, 19] in _sum_operands, 'The join Sum input is incorrect: %s.' % _sum_operands
```

### Step 3: Assign wf = pe.Workflow(...)

```python
wf = pe.Workflow(name='test')
```

**Verification:**
```python
assert [7, 9] in _sum_operands, 'The join Sum input is incorrect: %s.' % _sum_operands
```

### Step 4: Assign inputspec = pe.Node(...)

```python
inputspec = pe.Node(IdentityInterface(fields=['n']), name='inputspec')
```

### Step 5: Assign inputspec.iterables = value

```python
inputspec.iterables = [('n', [1, 2])]
```

### Step 6: Assign pre_join1 = pe.Node(...)

```python
pre_join1 = pe.Node(IncrementInterface(), name='pre_join1')
```

### Step 7: Call wf.connect()

```python
wf.connect(inputspec, 'n', pre_join1, 'input1')
```

### Step 8: Assign pre_join2 = pe.Node(...)

```python
pre_join2 = pe.Node(ProductInterface(), name='pre_join2')
```

### Step 9: Assign pre_join2.itersource = value

```python
pre_join2.itersource = ('inputspec', 'n')
```

### Step 10: Assign pre_join2.iterables = value

```python
pre_join2.iterables = ('input1', {1: [3, 4], 2: [5, 6]})
```

### Step 11: Call wf.connect()

```python
wf.connect(pre_join1, 'output1', pre_join2, 'input2')
```

### Step 12: Assign pre_join3 = pe.Node(...)

```python
pre_join3 = pe.Node(IncrementInterface(), name='pre_join3')
```

### Step 13: Call wf.connect()

```python
wf.connect(pre_join2, 'output1', pre_join3, 'input1')
```

### Step 14: Assign join = pe.JoinNode(...)

```python
join = pe.JoinNode(IdentityInterface(fields=['vector']), joinsource='pre_join2', joinfield='vector', name='join')
```

### Step 15: Call wf.connect()

```python
wf.connect(pre_join3, 'output1', join, 'vector')
```

### Step 16: Assign post_join1 = pe.Node(...)

```python
post_join1 = pe.Node(SumInterface(), name='post_join1')
```

### Step 17: Call wf.connect()

```python
wf.connect(join, 'vector', post_join1, 'input1')
```

### Step 18: Assign result = wf.run(...)

```python
result = wf.run()
```

**Verification:**
```python
assert len(result.nodes()) == 14, 'The number of expanded nodes is incorrect.'
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
'Test join on an input node which has an ``itersource``.'
tmpdir.chdir()
wf = pe.Workflow(name='test')
inputspec = pe.Node(IdentityInterface(fields=['n']), name='inputspec')
inputspec.iterables = [('n', [1, 2])]
pre_join1 = pe.Node(IncrementInterface(), name='pre_join1')
wf.connect(inputspec, 'n', pre_join1, 'input1')
pre_join2 = pe.Node(ProductInterface(), name='pre_join2')
pre_join2.itersource = ('inputspec', 'n')
pre_join2.iterables = ('input1', {1: [3, 4], 2: [5, 6]})
wf.connect(pre_join1, 'output1', pre_join2, 'input2')
pre_join3 = pe.Node(IncrementInterface(), name='pre_join3')
wf.connect(pre_join2, 'output1', pre_join3, 'input1')
join = pe.JoinNode(IdentityInterface(fields=['vector']), joinsource='pre_join2', joinfield='vector', name='join')
wf.connect(pre_join3, 'output1', join, 'vector')
post_join1 = pe.Node(SumInterface(), name='post_join1')
wf.connect(join, 'vector', post_join1, 'input1')
result = wf.run()
assert len(result.nodes()) == 14, 'The number of expanded nodes is incorrect.'
assert [16, 19] in _sum_operands, 'The join Sum input is incorrect: %s.' % _sum_operands
assert [7, 9] in _sum_operands, 'The join Sum input is incorrect: %s.' % _sum_operands
```

## Next Steps


---

*Source: test_join.py:453 | Complexity: Advanced | Last updated: 2026-05-18*