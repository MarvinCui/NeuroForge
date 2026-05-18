# How To: Sample Replacements

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test sample replacements

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `io`
- `operator`
- `warnings`
- `cloudpickle`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `pymc`
- `pymc.variational.opvi`
- `pymc.model.transform.basic`
- `pymc.pytensorf`
- `pymc.variational.inference`
- `pymc.variational.opvi`
- `tests`

**Setup Required:**
```python
# Fixtures: binomial_model_inference
```

## Step-by-Step Guide

### Step 1: Assign i = pt.iscalar(...)

```python
i = pt.iscalar()
```

**Verification:**
```python
assert any(map(operator.ne, sampled[1:], sampled[:-1]))
```

### Step 2: Assign approx = value

```python
approx = binomial_model_inference.approx
```

**Verification:**
```python
assert sampled.shape[0] == 100
```

### Step 3: Assign p = value

```python
p = approx.model.p
```

**Verification:**
```python
assert any(map(operator.ne, sampled[1:], sampled[:-1]))
```

### Step 4: Assign p_t = value

```python
p_t = p ** 3
```

**Verification:**
```python
assert sampled.shape[0] == 100
```

### Step 5: Assign p_s = approx.sample_node(...)

```python
p_s = approx.sample_node(p_t, size=100)
```

**Verification:**
```python
assert sampled.shape[0] == 101
```

### Step 6: Assign sampled = p_s.eval(...)

```python
sampled = p_s.eval()
```

**Verification:**
```python
assert any(map(operator.ne, sampled[1:], sampled[:-1]))
```

### Step 7: Assign p_d = approx.sample_node(...)

```python
p_d = approx.sample_node(p_t, size=i)
```

### Step 8: Assign sampled = p_d.eval(...)

```python
sampled = p_d.eval({i: 100})
```

**Verification:**
```python
assert any(map(operator.ne, sampled[1:], sampled[:-1]))
```

### Step 9: Assign sampled = p_d.eval(...)

```python
sampled = p_d.eval({i: 101})
```

**Verification:**
```python
assert sampled.shape[0] == 101
```


## Complete Example

```python
# Setup
# Fixtures: binomial_model_inference

# Workflow
i = pt.iscalar()
approx = binomial_model_inference.approx
p = approx.model.p
p_t = p ** 3
p_s = approx.sample_node(p_t, size=100)
sampled = p_s.eval()
assert any(map(operator.ne, sampled[1:], sampled[:-1]))
assert sampled.shape[0] == 100
p_d = approx.sample_node(p_t, size=i)
sampled = p_d.eval({i: 100})
assert any(map(operator.ne, sampled[1:], sampled[:-1]))
assert sampled.shape[0] == 100
sampled = p_d.eval({i: 101})
assert sampled.shape[0] == 101
```

## Next Steps


---

*Source: test_inference.py:311 | Complexity: Advanced | Last updated: 2026-05-18*