# How To: Callback Exception

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test callback exception

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `time`
- `json`
- `pytest`
- `nipype.interfaces.utility`
- `nipype.pipeline.engine`
- `logging`
- `os`
- `nipype.utils.profiler`
- `nipype.utils.draw_gantt_chart`

**Setup Required:**
```python
# Fixtures: tmpdir, plugin, stop_on_first_crash
```

## Step-by-Step Guide

### Step 1: Call tmpdir.chdir()

```python
tmpdir.chdir()
```

**Verification:**
```python
assert so.statuses == [('f_node', 'start'), ('f_node', 'exception')]
```

### Step 2: Assign so = Status(...)

```python
so = Status()
```

### Step 3: Assign wf = pe.Workflow(...)

```python
wf = pe.Workflow(name='test', base_dir=tmpdir.strpath)
```

### Step 4: Assign f_node = pe.Node(...)

```python
f_node = pe.Node(niu.Function(function=bad_func, input_names=[], output_names=[]), name='f_node')
```

### Step 5: Call wf.add_nodes()

```python
wf.add_nodes([f_node])
```

### Step 6: Assign unknown = value

```python
wf.config['execution'] = {'crashdump_dir': wf.base_dir, 'stop_on_first_crash': stop_on_first_crash, 'poll_sleep_duration': 2}
```

### Step 7: Call sleep()

```python
sleep(0.5)
```

**Verification:**
```python
assert so.statuses == [('f_node', 'start'), ('f_node', 'exception')]
```

### Step 8: Call wf.run()

```python
wf.run(plugin=plugin, plugin_args={'status_callback': so.callback})
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir, plugin, stop_on_first_crash

# Workflow
tmpdir.chdir()
so = Status()
wf = pe.Workflow(name='test', base_dir=tmpdir.strpath)
f_node = pe.Node(niu.Function(function=bad_func, input_names=[], output_names=[]), name='f_node')
wf.add_nodes([f_node])
wf.config['execution'] = {'crashdump_dir': wf.base_dir, 'stop_on_first_crash': stop_on_first_crash, 'poll_sleep_duration': 2}
with pytest.raises(Exception):
    wf.run(plugin=plugin, plugin_args={'status_callback': so.callback})
sleep(0.5)
assert so.statuses == [('f_node', 'start'), ('f_node', 'exception')]
```

## Next Steps


---

*Source: test_callback.py:46 | Complexity: Advanced | Last updated: 2026-05-18*