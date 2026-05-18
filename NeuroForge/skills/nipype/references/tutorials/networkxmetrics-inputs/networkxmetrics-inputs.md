# How To: Networkxmetrics Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test NetworkXMetrics inputs

## Prerequisites

**Required Modules:**
- `nx`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(compute_clique_related_measures=dict(usedefault=True), in_file=dict(extensions=None, mandatory=True), out_edge_metrics_matlab=dict(extensions=None, genfile=True), out_global_metrics_matlab=dict(extensions=None, genfile=True), out_k_core=dict(extensions=None, usedefault=True), out_k_crust=dict(extensions=None, usedefault=True), out_k_shell=dict(extensions=None, usedefault=True), out_node_metrics_matlab=dict(extensions=None, genfile=True), out_pickled_extra_measures=dict(extensions=None, usedefault=True), treat_as_weighted_graph=dict(usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(compute_clique_related_measures=dict(usedefault=True), in_file=dict(extensions=None, mandatory=True), out_edge_metrics_matlab=dict(extensions=None, genfile=True), out_global_metrics_matlab=dict(extensions=None, genfile=True), out_k_core=dict(extensions=None, usedefault=True), out_k_crust=dict(extensions=None, usedefault=True), out_k_shell=dict(extensions=None, usedefault=True), out_node_metrics_matlab=dict(extensions=None, genfile=True), out_pickled_extra_measures=dict(extensions=None, usedefault=True), treat_as_weighted_graph=dict(usedefault=True))
```

## Next Steps


---

*Source: test_auto_NetworkXMetrics.py:6 | Complexity: Beginner | Last updated: 2026-05-18*