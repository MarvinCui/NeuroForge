# How To: Clone Node Iterables

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test clone node iterables

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pytest`
- `base`
- `interfaces`
- `interfaces`

**Setup Required:**
```python
# Fixtures: tmpdir
```

## Step-by-Step Guide

### Step 1: Call tmpdir.chdir()

```python
tmpdir.chdir()
```

### Step 2: Assign subject_list = value

```python
subject_list = ['sub-001', 'sub-002']
```

### Step 3: Assign inputnode = pe.Node(...)

```python
inputnode = pe.Node(niu.IdentityInterface(fields=['subject']), name='inputnode')
```

### Step 4: Assign inputnode.iterables = value

```python
inputnode.iterables = [('subject', subject_list)]
```

### Step 5: Assign node_1 = pe.Node(...)

```python
node_1 = pe.Node(niu.Function(input_names='string', output_names='string', function=addstr), name='node_1')
```

### Step 6: Assign node_2 = node_1.clone(...)

```python
node_2 = node_1.clone('node_2')
```

### Step 7: Assign workflow = pe.Workflow(...)

```python
workflow = pe.Workflow(name='iter_clone_wf')
```

### Step 8: Call workflow.connect()

```python
workflow.connect([(inputnode, node_1, [('subject', 'string')]), (node_1, node_2, [('string', 'string')])])
```

### Step 9: Call workflow.run()

```python
workflow.run()
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
tmpdir.chdir()

def addstr(string):
    return '%s + 2' % string
subject_list = ['sub-001', 'sub-002']
inputnode = pe.Node(niu.IdentityInterface(fields=['subject']), name='inputnode')
inputnode.iterables = [('subject', subject_list)]
node_1 = pe.Node(niu.Function(input_names='string', output_names='string', function=addstr), name='node_1')
node_2 = node_1.clone('node_2')
workflow = pe.Workflow(name='iter_clone_wf')
workflow.connect([(inputnode, node_1, [('subject', 'string')]), (node_1, node_2, [('string', 'string')])])
workflow.run()
```

## Next Steps


---

*Source: test_base.py:67 | Complexity: Advanced | Last updated: 2026-05-18*