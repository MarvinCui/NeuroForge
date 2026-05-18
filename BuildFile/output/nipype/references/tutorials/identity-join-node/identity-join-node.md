# How To: Identity Join Node

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test an IdentityInterface join.

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

### Step 1: 'Test an IdentityInterface join.'

```python
'Test an IdentityInterface join.'
```

**Verification:**
```python
assert len(result.nodes()) == 5, 'The number of expanded nodes is incorrect.'
```

### Step 2: Assign _sum_operands = value

```python
_sum_operands = []
```

**Verification:**
```python
assert _sum_operands[0] == [2, 3, 4], 'The join Sum input is incorrect: %s.' % _sum_operands[0]
```

### Step 3: Call tmpdir.chdir()

```python
tmpdir.chdir()
```

### Step 4: Assign wf = pe.Workflow(...)

```python
wf = pe.Workflow(name='test')
```

### Step 5: Assign inputspec = pe.Node(...)

```python
inputspec = pe.Node(IdentityInterface(fields=['n']), name='inputspec')
```

### Step 6: Assign inputspec.iterables = value

```python
inputspec.iterables = [('n', [1, 2, 3])]
```

### Step 7: Assign pre_join1 = pe.Node(...)

```python
pre_join1 = pe.Node(IncrementInterface(), name='pre_join1')
```

### Step 8: Call wf.connect()

```python
wf.connect(inputspec, 'n', pre_join1, 'input1')
```

### Step 9: Assign join = pe.JoinNode(...)

```python
join = pe.JoinNode(IdentityInterface(fields=['vector']), joinsource='inputspec', joinfield='vector', name='join')
```

### Step 10: Call wf.connect()

```python
wf.connect(pre_join1, 'output1', join, 'vector')
```

### Step 11: Assign post_join1 = pe.Node(...)

```python
post_join1 = pe.Node(SumInterface(), name='post_join1')
```

### Step 12: Call wf.connect()

```python
wf.connect(join, 'vector', post_join1, 'input1')
```

### Step 13: Assign result = wf.run(...)

```python
result = wf.run()
```

**Verification:**
```python
assert len(result.nodes()) == 5, 'The number of expanded nodes is incorrect.'
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
'Test an IdentityInterface join.'
global _sum_operands
_sum_operands = []
tmpdir.chdir()
wf = pe.Workflow(name='test')
inputspec = pe.Node(IdentityInterface(fields=['n']), name='inputspec')
inputspec.iterables = [('n', [1, 2, 3])]
pre_join1 = pe.Node(IncrementInterface(), name='pre_join1')
wf.connect(inputspec, 'n', pre_join1, 'input1')
join = pe.JoinNode(IdentityInterface(fields=['vector']), joinsource='inputspec', joinfield='vector', name='join')
wf.connect(pre_join1, 'output1', join, 'vector')
post_join1 = pe.Node(SumInterface(), name='post_join1')
wf.connect(join, 'vector', post_join1, 'input1')
result = wf.run()
assert len(result.nodes()) == 5, 'The number of expanded nodes is incorrect.'
assert _sum_operands[0] == [2, 3, 4], 'The join Sum input is incorrect: %s.' % _sum_operands[0]
```

## Next Steps


---

*Source: test_join.py:335 | Complexity: Advanced | Last updated: 2026-05-18*