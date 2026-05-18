# How To: Signatures With Doc In Child

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test signatures with doc in child

## Prerequisites

**Required Modules:**
- `__future__`
- `mdp`
- `inspect`


## Step-by-Step Guide

### Step 1: Assign anode = AncestorNode(...)

```python
anode = AncestorNode()
```

**Verification:**
```python
assert anode.foo == 42
```

### Step 2: Call anode.train()

```python
anode.train(X, foo='abc')
```

**Verification:**
```python
assert get_signature(anode.train) == 'self, x, foo'
```

### Step 3: Assign cnode = ChildNode(...)

```python
cnode = ChildNode()
```

**Verification:**
```python
assert cnode.train.__doc__ == 'doc child'
```

### Step 4: Call cnode.train()

```python
cnode.train(X, foo2='abc')
```

**Verification:**
```python
assert cnode.foo2 == 42
```

### Step 5: Assign self.foo = 42

```python
self.foo = 42
```

**Verification:**
```python
assert get_signature(cnode.train) == 'self, x, foo2'
```

### Step 6: """doc child"""

```python
"""doc child"""
```

### Step 7: Assign self.foo2 = 42

```python
self.foo2 = 42
```


## Complete Example

```python
# Workflow
class AncestorNode(mdp.Node):

    def _train(self, x, foo=None):
        self.foo = 42
anode = AncestorNode()
anode.train(X, foo='abc')
assert anode.foo == 42
assert get_signature(anode.train) == 'self, x, foo'

class ChildNode(AncestorNode):

    def _train(self, x, foo2=None):
        """doc child"""
        self.foo2 = 42
cnode = ChildNode()
assert cnode.train.__doc__ == 'doc child'
cnode.train(X, foo2='abc')
assert cnode.foo2 == 42
assert get_signature(cnode.train) == 'self, x, foo2'
```

## Next Steps


---

*Source: test_node_metaclass.py:106 | Complexity: Intermediate | Last updated: 2026-05-18*