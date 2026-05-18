# How To: Networkxmetrics Outputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test NetworkXMetrics outputs

## Prerequisites

**Required Modules:**
- `nx`


## Step-by-Step Guide

### Step 1: Assign output_map = dict(...)

```python
output_map = dict(edge_measure_networks=dict(), edge_measures_matlab=dict(extensions=None), global_measures_matlab=dict(extensions=None), gpickled_network_files=dict(), k_core=dict(extensions=None), k_crust=dict(extensions=None), k_networks=dict(), k_shell=dict(extensions=None), matlab_dict_measures=dict(), matlab_matrix_files=dict(), node_measure_networks=dict(), node_measures_matlab=dict(extensions=None), pickled_extra_measures=dict(extensions=None))
```


## Complete Example

```python
# Workflow
output_map = dict(edge_measure_networks=dict(), edge_measures_matlab=dict(extensions=None), global_measures_matlab=dict(extensions=None), gpickled_network_files=dict(), k_core=dict(extensions=None), k_crust=dict(extensions=None), k_networks=dict(), k_shell=dict(extensions=None), matlab_dict_measures=dict(), matlab_matrix_files=dict(), node_measure_networks=dict(), node_measures_matlab=dict(extensions=None), pickled_extra_measures=dict(extensions=None))
```

## Next Steps


---

*Source: test_auto_NetworkXMetrics.py:54 | Complexity: Beginner | Last updated: 2026-05-18*