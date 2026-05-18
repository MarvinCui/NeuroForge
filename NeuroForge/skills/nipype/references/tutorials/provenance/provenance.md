# How To: Provenance

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test provenance

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `copy`
- `pytest`
- `interfaces`
- `interfaces`
- `utils`
- `shutil`
- `numpy`

**Setup Required:**
```python
# Fixtures: tmpdir
```

## Step-by-Step Guide

### Step 1: Assign metawf = pe.Workflow(...)

```python
metawf = pe.Workflow(name='meta')
```

**Verification:**
```python
assert len(psg.bundles) == 2
```

### Step 2: Assign metawf.base_dir = value

```python
metawf.base_dir = tmpdir.strpath
```

**Verification:**
```python
assert len(psg.get_records()) == 7
```

### Step 3: Call metawf.add_nodes()

```python
metawf.add_nodes([create_wf('wf%d' % i) for i in range(1)])
```

### Step 4: Assign eg = metawf.run(...)

```python
eg = metawf.run(plugin='Linear')
```

### Step 5: Assign prov_base = value

```python
prov_base = tmpdir.join('workflow_provenance_test').strpath
```

### Step 6: Assign psg = write_workflow_prov(...)

```python
psg = write_workflow_prov(eg, prov_base, format='all')
```

**Verification:**
```python
assert len(psg.bundles) == 2
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
metawf = pe.Workflow(name='meta')
metawf.base_dir = tmpdir.strpath
metawf.add_nodes([create_wf('wf%d' % i) for i in range(1)])
eg = metawf.run(plugin='Linear')
prov_base = tmpdir.join('workflow_provenance_test').strpath
psg = write_workflow_prov(eg, prov_base, format='all')
assert len(psg.bundles) == 2
assert len(psg.get_records()) == 7
```

## Next Steps


---

*Source: test_utils.py:156 | Complexity: Intermediate | Last updated: 2026-05-18*