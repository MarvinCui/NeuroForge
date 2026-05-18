# How To: Function Profiling

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test runtime profiler correctly records workflow RAM/CPUs consumption
of a Function interface

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `pytest`
- `utils.profiler`
- `base`
- `nipype`
- `nipype`
- `nipype`

**Setup Required:**
```python
# Fixtures: tmpdir, mem_gb, n_procs, use_resource_monitor
```

## Step-by-Step Guide

### Step 1: '\n    Test runtime profiler correctly records workflow RAM/CPUs consumption\n    of a Function interface\n    '

```python
'\n    Test runtime profiler correctly records workflow RAM/CPUs consumption\n    of a Function interface\n    '
```

**Verification:**
```python
assert abs(mem_gb - result.runtime.mem_peak_gb) < 0.3, 'estimated memory error above .3GB'
```

### Step 2: Call config.set()

```python
config.set('monitoring', 'sample_frequency', '0.2')
```

**Verification:**
```python
assert int(result.runtime.cpu_percent / 100 + 0.2) >= n_procs
```

### Step 3: Call tmpdir.chdir()

```python
tmpdir.chdir()
```

### Step 4: Assign iface = niu.Function(...)

```python
iface = niu.Function(function=_use_resources)
```

### Step 5: Assign iface.inputs.mem_gb = mem_gb

```python
iface.inputs.mem_gb = mem_gb
```

### Step 6: Assign iface.inputs.n_procs = n_procs

```python
iface.inputs.n_procs = n_procs
```

### Step 7: Assign result = iface.run(...)

```python
result = iface.run()
```

**Verification:**
```python
assert abs(mem_gb - result.runtime.mem_peak_gb) < 0.3, 'estimated memory error above .3GB'
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir, mem_gb, n_procs, use_resource_monitor

# Workflow
'\n    Test runtime profiler correctly records workflow RAM/CPUs consumption\n    of a Function interface\n    '
from nipype import config
config.set('monitoring', 'sample_frequency', '0.2')
tmpdir.chdir()
iface = niu.Function(function=_use_resources)
iface.inputs.mem_gb = mem_gb
iface.inputs.n_procs = n_procs
result = iface.run()
assert abs(mem_gb - result.runtime.mem_peak_gb) < 0.3, 'estimated memory error above .3GB'
assert int(result.runtime.cpu_percent / 100 + 0.2) >= n_procs
```

## Next Steps


---

*Source: test_resource_monitor.py:84 | Complexity: Intermediate | Last updated: 2026-05-18*