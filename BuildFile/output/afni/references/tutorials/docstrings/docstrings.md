# How To: Docstrings

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test docstrings

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
assert anode.train.__doc__ == 'doc ancestor'
```

### Step 2: Call anode.train()

```python
anode.train(X)
```

**Verification:**
```python
assert anode.foo == 42
```

### Step 3: Assign cnode = ChildNode(...)

```python
cnode = ChildNode()
```

**Verification:**
```python
assert get_signature(anode.train) == 'self, x'
```

### Step 4: Call cnode.train()

```python
cnode.train(X)
```

**Verification:**
```python
assert cnode.train.__doc__ == 'doc child'
```

### Step 5: """doc ancestor"""

```python
"""doc ancestor"""
```

**Verification:**
```python
assert cnode.foo2 == 42
```

### Step 6: Assign self.foo = 42

```python
self.foo = 42
```

**Verification:**
```python
assert get_signature(cnode.train) == 'self, x'
```

### Step 7: """doc child"""

```python
"""doc child"""
```

### Step 8: Assign self.foo2 = 42

```python
self.foo2 = 42
```


## Complete Example

```python
# Workflow
class AncestorNode(mdp.Node):

    def _train(self, x):
        """doc ancestor"""
        self.foo = 42
anode = AncestorNode()
assert anode.train.__doc__ == 'doc ancestor'
anode.train(X)
assert anode.foo == 42
assert get_signature(anode.train) == 'self, x'

class ChildNode(AncestorNode):

    def _train(self, x):
        """doc child"""
        self.foo2 = 42
cnode = ChildNode()
assert cnode.train.__doc__ == 'doc child'
cnode.train(X)
assert cnode.foo2 == 42
assert get_signature(cnode.train) == 'self, x'
```

## Next Steps


---

*Source: test_node_metaclass.py:12 | Complexity: Advanced | Last updated: 2026-05-18*