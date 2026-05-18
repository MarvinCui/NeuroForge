# How To: Callback Gantt

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test callback gantt

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
# Fixtures: tmp_path, plugin
```

## Step-by-Step Guide

### Step 1: Assign log_filename = value

```python
log_filename = tmp_path / 'callback.log'
```

**Verification:**
```python
assert (tmp_path / 'callback.log.html').exists()
```

### Step 2: Assign logger = logging.getLogger(...)

```python
logger = logging.getLogger('callback')
```

### Step 3: Call logger.setLevel()

```python
logger.setLevel(logging.DEBUG)
```

### Step 4: Assign handler = logging.FileHandler(...)

```python
handler = logging.FileHandler(log_filename)
```

### Step 5: Call logger.addHandler()

```python
logger.addHandler(handler)
```

### Step 6: Assign wf = pe.Workflow(...)

```python
wf = pe.Workflow(name='test', base_dir=str(tmp_path))
```

### Step 7: Assign f_node = pe.Node(...)

```python
f_node = pe.Node(niu.Function(function=func, input_names=[], output_names=[]), name='f_node')
```

### Step 8: Call wf.add_nodes()

```python
wf.add_nodes([f_node])
```

### Step 9: Assign unknown = value

```python
wf.config['execution'] = {'crashdump_dir': wf.base_dir, 'poll_sleep_duration': 2}
```

### Step 10: Assign plugin_args = value

```python
plugin_args = {'status_callback': log_nodes_cb}
```

### Step 11: Call wf.run()

```python
wf.run(plugin=plugin, plugin_args=plugin_args)
```

### Step 12: Assign first_line = json.loads(...)

```python
first_line = json.loads(loglines[0])
```

### Step 13: Assign unknown = value

```python
loglines[0] = f'{json.dumps(first_line)}\n'
```

### Step 14: Call loglines.append()

```python
loglines.append(loglines[-1])
```

**Verification:**
```python
assert (tmp_path / 'callback.log.html').exists()
```

### Step 15: Assign unknown = 8

```python
plugin_args['n_procs'] = 8
```

### Step 16: Assign loglines = _f.readlines(...)

```python
loglines = _f.readlines()
```

### Step 17: Call _f.write()

```python
_f.write(''.join(loglines))
```

### Step 18: Call generate_gantt_chart()

```python
generate_gantt_chart(str(log_filename), 1 if plugin == 'Linear' else 8)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, plugin

# Workflow
import logging
from os import path
from nipype.utils.profiler import log_nodes_cb
from nipype.utils.draw_gantt_chart import generate_gantt_chart
log_filename = tmp_path / 'callback.log'
logger = logging.getLogger('callback')
logger.setLevel(logging.DEBUG)
handler = logging.FileHandler(log_filename)
logger.addHandler(handler)
wf = pe.Workflow(name='test', base_dir=str(tmp_path))
f_node = pe.Node(niu.Function(function=func, input_names=[], output_names=[]), name='f_node')
wf.add_nodes([f_node])
wf.config['execution'] = {'crashdump_dir': wf.base_dir, 'poll_sleep_duration': 2}
plugin_args = {'status_callback': log_nodes_cb}
if plugin != 'Linear':
    plugin_args['n_procs'] = 8
wf.run(plugin=plugin, plugin_args=plugin_args)
with open(log_filename, 'r') as _f:
    loglines = _f.readlines()
first_line = json.loads(loglines[0])
if 'duration' in first_line:
    del first_line['duration']
loglines[0] = f'{json.dumps(first_line)}\n'
loglines.append(loglines[-1])
with open(log_filename, 'w') as _f:
    _f.write(''.join(loglines))
with pytest.warns(Warning):
    generate_gantt_chart(str(log_filename), 1 if plugin == 'Linear' else 8)
assert (tmp_path / 'callback.log.html').exists()
```

## Next Steps


---

*Source: test_callback.py:68 | Complexity: Advanced | Last updated: 2026-05-18*